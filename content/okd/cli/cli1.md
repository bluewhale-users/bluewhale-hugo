---
title: "CLI : oc 설정"
date: 2022-03-31T15:22:13+09:00
draft: false
weight: 41
---

- [okd github](https://github.com/openshift/okd)  
- [okd documentation](https://docs.okd.io/latest/cli_reference/openshift_cli/getting-started-cli.html#cli-getting-started)  
- [oc download](https://github.com/openshift/okd/releases)  

### 1. oc download
- [oc download](https://github.com/openshift/okd/releases)  
- OS에 맞게 실행파일을 다운로드한다. 

### 2. 압축 해제
- 적당한 경로에 압축을 해제한다. 

### 3. 환경변수 편집
* 환경변수에 경로 추가  
  * window + Q로 검색창을 연 뒤 환경 변수를 검색해서 환경 변수 선택  
  * 시스템변수의 Path를 더블클릭한다.  
  * 새로 만들기를 클릭한 다음 아까 압축을 풀었던 곳의 경로를 등록  
* command에서 oc version을 쳐서 확인


{{< tabs >}}
{{% tab name="windows" %}}
```windows
C:\Users\user>oc version
Client Version: 4.8.0-0.okd-2021-11-14-052418
error: You must be logged in to the server (Unauthorized)
```
{{% /tab %}}
{{% tab name="MacOS" %}}
```Bash
brew install openshift-cli
```
{{% /tab %}}
{{< /tabs >}}

### 4. 로그인
```
oc login [URL] [options]
```

{{< tabs >}}
{{% tab name="windows" %}}
```windows
C:\Users\user>oc login --token=sha256~HH2JyDxeBpYg******************** --server=https://api.your-okd.com:6443
Logged into "api.your-okd.com:6443" as "user@your-okd.com" using the token provided.

You have access to 97 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "okd-tutorial".
```
{{% /tab %}}
{{< /tabs >}}

{{% notice tip %}}
-p, --password = " − Password, will prompt if not provided  
-u, --username = " − Username, will prompt if not provided  
--certificate-authority = " − Path to a cert. file for the certificate authority  
--insecure-skip-tls-verify = false − If true, the server's certificate will not be checked for validity. This will make your HTTPS connections insecure  
--token = " − Bearer token for authentication to the API server  
To get the complete details regarding any command, use the oc <Command Name> --help command.  
{{% /notice %}}