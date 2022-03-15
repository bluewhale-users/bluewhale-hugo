---
title: "Tutorial12"
date: 2022-03-15T11:33:14+09:00
weight: 52
---

# Private Repository 연동

## 1. SSH 키 생성
``` 
- Git Bash 실행
- 사용자 폴더로 이동후 .ssh 폴더 생성 및 이동
- ssh-keygen 실행
```

## ssh-keygen 사용시 기본값(SHA-1)은 github에서 더 이상 인증 용도로 사용할 수 없다. 
Update : 2022-01-11  
November 16, 2021	The ECDSA and Ed25519 host keys will start to be fully usable. GitHub’s DSA host key will no longer be supported.

```
Unable to connect SSH repository: unknown error: ERROR: You're using an RSA key with SHA-1, which is no longer allowed. Please use a newer client or a different key type.
```
```
https://github.blog/2021-09-01-improving-git-protocol-security-github/

- Removing support for all DSA keys
- Adding requirements for newly added RSA keys
- Removing some legacy SSH algorithms (HMAC-SHA-1 and CBC ciphers)
- Adding ECDSA and Ed25519 host keys for SSH
Turning off the unencrypted Git protocol

github 지원 타입
'ssh-rsa', 'ecdsa-sha2-nistp256', 'ecdsa-sha2-nistp384', 'ecdsa-sha2-nistp521', 'ssh-ed25519', 'sk-ecdsa-sha2-nistp256@openssh.com', 'sk-ssh-ed25519@openssh.com'.  

아래 타입으로 생성
ssh-keygen -t ecdsa-sha2-nistp521
```

```
$ ssh-keygen -t ecdsa-sha2-nistp521
Generating public/private ecdsa-sha2-nistp521 key pair.
Enter file in which to save the key (/c/Users/owner/.ssh/id_ecdsa): blackwhale-testuser-nistp521-id
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in blackwhale-testuser-nistp521-id.
Your public key has been saved in blackwhale-testuser-nistp521-id.pub.
The key fingerprint is:
SHA256:XwWVH/MoeDVvW6UGGUru6gGnPMoHv7bRU+cvKNs68BY owner@DESKTOP-2M4EABD
The key's randomart image is:
+---[ECDSA 521]---+
|          . o+.. |
|         o .o.+o.|
|          o. o.*=|
|         .. o.+ *|
|      . S o.oo .o|
|    ...=E+ +   . |
|     o=o=....    |
|   . .++=+. ..   |
|    ooo++=.  ..  |
+----[SHA256]-----+

```

{{< figure src="/cicd/tutorial12_1.jpg" >}}
{{< figure src="/cicd/tutorial12_2.jpg" >}}

## 2. Github Private Repository 설정  
### User profile에서 Settings 이동
{{< figure src="/cicd/tutorial12_3.jpg" >}}

### SSH and GPG Keys 설정으로 이동  
{{< figure src="/cicd/tutorial12_4.jpg" >}}

### New SSH key 선택후 생성한 testuser_id.pub 파일을 메모장으로 열어 모두 복사후 붙여넣기
{{< figure src="/cicd/tutorial12_5.jpg" >}}

## 3. Repository Clone 방법
- "사용자 폴더"/.ssh/config 파일을 만든다. 
{{< figure src="/cicd/tutorial12_6.jpg" >}}

- 생성한 키를 아래 형식으로 추가한다. 
```
Host testuser_github
        Hostname github.com
    User git
        IdentityFile=C:\Users\owner\.ssh\testuser_id
```

- git clone
```
git clone testuser_github:blackwhale-testuser/privatetutorial.git
```
[output]
```
C:\Work2021\spcsenti2023>git
clone testuser_github:blackwhale-testuser/privatetutorial.git
Cloning into 'privatetutorial'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

## Jenkins Private Repository 설정 방법
- Deploy Key 생성
```
SSH 키 생성
Git Bash 실행
사용자 폴더로 이동후 .ssh 폴더 생성 및 이동
ssh-keygen 실행
```
### ssh key 생성  
{{< figure src="/cicd/tutorial12_8.jpg" >}}
{{< figure src="/cicd/tutorial12_9.jpg" >}}

### GitHub private repository로 이동하여, Settings의 Deploy Keys를 선택한다. 
{{< figure src="/cicd/tutorial12_10.jpg" >}}

### 생성한 Public Key를 메모장으로 열어 모두 복사후 붙여 넣는다. 
{{< figure src="/cicd/tutorial12_11.jpg" >}}

## Jenkins 설정
```
- Jenkins →  Jenkins 관리 → Manage Credentials 이동
- (global) 도메인 선택
```
{{< figure src="/cicd/tutorial12_12.jpg" >}}

```
Add Credentials 선택
Kind를 SSH Username with private key 선택
ID와 Username을 입력
Privte Key에서 Enter directly를 선택후 Add를 눌러 생성한 Private Key를 메모장으로 열어 모두 복사후 붙여넣는다. 
```
{{< figure src="/cicd/tutorial12_13.jpg" >}}

```
파이프라인 생성과정은 동일
GitHub Repository에서 SSH Clone 주소를 확인한다. 
git@github.com:blackwhale-testuser/privatetutorial.git
```
{{< figure src="/cicd/tutorial12_14.jpg" >}}

```
Pipeline 설정에서 Repository URL을 위에서 확인한 주소로 넣는다. 
Credentials에서 본인이 생성한 Credential을 선택한다. 
```
{{< figure src="/cicd/tutorial12_15.jpg" >}}

## ArgoCD Private Repository 설정 방법
### ArgoCD 이동후 Settings → Repositories 이동
{{< figure src="/cicd/tutorial12_16.jpg" >}}

```
- CONNECT REPO USING SSH 선택
- 로컬에서 생성한 Private Key를 메모장으로 열어 모두 복사후 SSH private key data에 붙여 넣는다. 
- Skip server verification 체크
- Enable LFS support(Git only) 체크
- Connect를 누른다. 
- Connection Status가 Successful인지 확인
```
{{< figure src="/cicd/tutorial12_17.jpg" >}}

```
GitHub Private repository SSH 주소를 확인한다. 
git@github.com:blackwhale-testuser/privatetutorial.git
```
{{< figure src="/cicd/tutorial12_18.jpg" >}}

```
App 생성시 Source의 Repository URL에 ssh 주소를 입력한다. 
```
{{< figure src="/cicd/tutorial12_19.jpg" >}}