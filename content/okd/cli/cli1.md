---
title: "CLI : oc 설정"
date: 2022-03-31T15:22:13+09:00
draft: false
weight: 41
---

- [okd github](https://github.com/openshift/okd)  
- [okd documentation](https://docs.okd.io/latest/cli_reference/openshift_cli/getting-started-cli.html#cli-getting-started)  
- [oc download](https://github.com/openshift/okd/releases)  


{{% notice tip %}}
Kubernetes의 명령줄 인터페이스(CLI) kubectl는 Kubernetes 클러스터에 대해 명령을 실행하는 데 사용됩니다. 
OKD는 Kubernetes 클러스터 위에서 실행되기 때문에 kubectl도 oc CLI에 포함됩니다.
{{% /notice %}}

### 1. oc download
- [oc download](https://github.com/openshift/okd/releases)  
  - OS에 맞게 실행파일을 다운로드한다. 
- OKD web-console에서 직접 다운로드
  - 우측 상단의 about 링크를 눌러 Command line tools로 이동해 다운로드 받을 수 있다.  

{{< figure src="/cli/cli1_1.jpg#floatleft" >}}   
{{< figure src="/cli/cli1_2.jpg" >}}   

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


### 5. 로그아웃
```
oc logout
```

```
$ oc logout
Logged "user@your-okd.com" out on "https://api.your-okd.com:6443"
```

### 6. CLI Configuration Files
- CLI Configuration file을 통해 사용자 정보를 관리하며 여러 프로필을 설정해 전환이 가능한다. 
- "~/.kube/config"에 저장된다. 

```
$ oc config view
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server: https://api.your-okd.com:6443
  name: api.your-okd.com:6443
contexts:
- context:
    cluster: api.your-okd.com:6443
    namespace: tutorial-project
    user: user@your-okd.com/api.your-okd.com:6443
  name: tutorial-project/api.your-okd.com:6443/user@your-okd.com
current-context: nginx-proxy/api.your-okd.com:6443/user@your-okd.com
kind: Config
preferences: {}
users:
- name: user@your-okd.com/api.your-okd.com:6443
  user:
    token: REDACTED
```

- context 조회
```
$ oc whoami -c
nginx-proxy/api.your-okd.com:6443/user@your-okd.com
```

### 7. oc status 명령
- 프로젝트의 구성 요소 및 관계등을 파악할수 있다. 
``` command
$ oc status
In project nginx-proxy on server https://api.your-okd.com:6443

svc/argocd-sample-dex-server - 172.30.46.161 ports 5556, 5557
  deployment/argocd-sample-dex-server deploys ghcr.io/dexidp/dex@sha256:6b3cc1c385fbc7542244614e4432f2546c619b7850d44d2379c598309a06bed8
    deployment #3 running for 4 weeks - 1 pod
    deployment #2 deployed 2 months ago
    deployment #1 deployed 3 months ago

svc/argocd-sample-metrics - 172.30.232.17:8082
  statefulset/argocd-sample-application-controller manages quay.io/argoproj/argocd@sha256:bac1aeee8e78e64d81a633b9f64148274abfa003165544354e2ebf1335b6ee73
    created 3 months ago - 1 pod

svc/argocd-sample-redis - 172.30.61.181:6379
  deployment/argocd-sample-redis deploys redis@sha256:4be7fdb131e76a6c6231e820c60b8b12938cf1ff3d437da4871b9b2440f4e385
    deployment #1 running for 3 months - 1 pod

svc/argocd-sample-repo-server - 172.30.216.33 ports 8081, 8084
  deployment/argocd-sample-repo-server deploys quay.io/argoproj/argocd@sha256:bac1aeee8e78e64d81a633b9f64148274abfa003165544354e2ebf1335b6ee73
    deployment #3 running for 4 weeks - 1 pod
    deployment #2 deployed 2 months ago
    deployment #1 deployed 3 months ago

svc/argocd-sample-server-metrics - 172.30.21.153:8083
https://argocd-sample-server-nginx-proxy.apps.blackwhale.cloud.hancom.com (passthrough) to pod port https (svc/argocd-sample-server)
  deployment/argocd-sample-server deploys quay.io/argoproj/argocd@sha256:bac1aeee8e78e64d81a633b9f64148274abfa003165544354e2ebf1335b6ee73
    deployment #3 running for 4 weeks - 1 pod
    deployment #2 deployed 2 months ago
    deployment #1 deployed 3 months ago

http://nginx-sample-nginx-proxy.apps.blackwhale.cloud.hancom.com to pod port 8080-tcp (svc/nginx-sample)
  deployment/nginx-sample deploys istag/nginx-sample:latest
    deployment #2 running for 4 months - 1 pod
    deployment #1 deployed 4 months ago

deployment/argo-tag-test deploys orca-harbor.cloud.hancom.com/test-harbor/tag:latest
  deployment #2 running for 3 months - 0/1 pods
  deployment #1 deployed 3 months ago

bc/nginx-sample source builds https://github.com/sclorg/nginx-ex.git on openshift/nginx:1.18-ubi7
  -> istag/nginx-sample:$OPENSHIFT_BUILD_COMMIT
  build #4 failed 3 months ago - 65a79f2: Merge pull request #23 from multi-arch/imagestreams (Petr Hracek <phracek@redhat.com>)
  build #1 succeeded 4 months ago - 65a79f2: Merge pull request #23 from multi-arch/imagestreams (Petr Hracek <phracek@redhat.com>)

Errors:
  * build/nginx-sample-4 has failed.

1 error, 12 warnings, 4 infos identified, use 'oc status --suggest' to see details.
```