---
title: "Tutorial10 : GitHub Webhook 추가"
date: 2022-03-15T11:32:53+09:00
weight: 50
---

## CI/CD

### 1. GitHub Source Repository에 Webhook 추가
- [Source Repositoy](https://github.com/blackwhale-testuser/okd-tutorial1-src)

#### 1.1 Settings -> Webhooks 이동후 Add Webhook 선택
{{< figure src="/cicd/tutorial10_1.jpg" >}}  

#### 1.2 jenkins 주소를 확인후 payload url에 입력
{{< figure src="/cicd/tutorial10_2.jpg" >}}  

{{% notice info %}}
Payload URL : https://jenkins-okd-tutorial.apps.blackwhale.cloud.hancom.com/github-webhook/  
Content type : application/json  
Trigger : Juste the push event  
{{% /notice %}}

#### 1.3 소스 수정후 commit
{{% notice tip %}}
Jenkinsfile의 태그를 업데이트 해야 GitOps Repo로 Commit 할 수 있다.   
sed -i 's/MY_BUILD_TAG/$BUILD_NUMBER/' testblog-deployment.yaml  
BUILD_NUMBER가 정상적으로 셋팅되는지 확인  
{{% /notice %}}
{{< figure src="/cicd/tutorial10_3.jpg" >}}  

#### 1.4 Jenkins 빌드가 자동으로 동작하는지 확인
{{< figure src="/cicd/tutorial10_4.jpg" >}}  

### 2. ArgoCD Auto-Sync
{{% notice info %}}
Applications -> "Your Application" 이동후 App Details 선택  
SYNC-POLICY : Enable Auto-Sync 선택  
{{% /notice %}}
{{< figure src="/cicd/tutorial10_5.jpg" >}}