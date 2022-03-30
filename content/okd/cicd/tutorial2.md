---
title: "Tutorial2 : 리파지터리 생성"
date: 2022-03-15T11:27:51+09:00
draft: false
weight: 42
---

## GitHub Repository 준비

### origin repository
- [src](https://github.com/bluewhale-users/okd-tutorial1-src)
- [gitops](https://github.com/bluewhale-users/okd-tutorial1-gitops)

  
### 1. 2개 리파지터리를 본인 계정으로 fork
{{< figure src="/cicd/tutorial2_1.jpg" >}}

- [src fork repo](https://github.com/blackwhale-testuser/okd-tutorial1-src)
- [gitops fork repo](https://github.com/blackwhale-testuser/okd-tutorial1-gitops)

### 2. Deploy Key 생성 및 등록
jenkins 빌드후 gitops 리파지터리에 commit을 수행하기 위해 deploy key를 등록합니다.

#### 2.1 Gitbash를 실행하여 ssh-keygen을 통해 deploy key를 생성
```
user@DESKTOP-1RAT70A MINGW64 ~/.ssh
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa): okd-tutorial-deploykey
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in okd-tutorial-deploykey.
Your public key has been saved in okd-tutorial-deploykey.pub.
The key fingerprint is:
SHA256:AnFXcqY8jKZ9T3XTp12eh5cJd7ofMmRYMOml5gFZjao user@DESKTOP-1RAT70A
The key's randomart image is:
+---[RSA 3072]----+
|    . . o.*++    |
|     o = B ooo . |
|    . o = + +oo.=|
|     =   o *o.oBB|
|    . o S +..o++=|
|       E o .o  o.|
|          .  o.. |
|              o..|
|                .|
+----[SHA256]-----+
```

### 3. [GitOps Repo](https://github.com/blackwhale-testuser/okd-tutorial1-gitops) 이동
{{< figure src="/cicd/tutorial2_2.jpg" >}}

#### 3.1 Settings -> Deploy keys로 이동해 Add deploy key 선택(Allow write access 체크)
{{< figure src="/cicd/tutorial2_3.jpg" >}}
{{< figure src="/cicd/tutorial2_4.jpg" >}}

### 4. [Source Repo](https://github.com/blackwhale-testuser/okd-tutorial1-src) 이동

#### 4.1 Jenkins 파일 편집

``` diff
......
stage("Update Tag") { 
    steps {
    checkout([$class: 'GitSCM',
                    branches: [[name: '*/master' ]],
                    extensions: scm.extensions,
                    userRemoteConfigs: [[                         
-                   url: 'fork한 repo url',         
+                   url: 'git@github.com:blackwhale-testuser/okd-tutorial1-gitops.git', 
                    credentialsId: 'jenkins-ssh-private',
                    ]]
            ])
    sshagent(credentials: ['jenkins-ssh-private']){
        sh("""
            #!/usr/bin/env bash
            set +x
            export GIT_SSH_COMMAND="ssh -oStrictHostKeyChecking=no"
            git config --global user.email "test@gmail.com"
            git checkout master
            cp --f base/deployment-sample.yaml okd-deploy/temp.yaml
            cd okd-deploy
            sed -i 's/MY_BUILD_TAG/test.4/' temp.yaml 
            cat temp.yaml
            cp --f temp.yaml testblog-deployment.yaml 
            git commit -a -m "updated the image tag"
            git push
        """)
    }
    }
}
......
```