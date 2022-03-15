---
title: "Tutorial1"
date: 2022-03-15T10:47:32+09:00
weight: 41
---

# OKD CI/CD Tutorial

{{< figure src="/cicd/tutorial1_1.jpg" title="CI/CD Flow with Argo CD" >}}   
[출처] https://www.gspann.com/resources/blogs/continuous-delivery-for-kubernetes-with-gitops-and-argo-cd/


```
'GitOps'는 형상 관리 도구인 'Git' 을 통해 개발자에게 익숙한 방식으로 인프라 또는 
어플리케이션의 선언적인 설정파일을 관리하고 배포하는 일련의 프로세스를 말한다.

튜토리얼은 2개의 리파지토리가 필요하다. 

어플리케이션 소스를 담고있는 Source Repository
OKD에 배포설정(manifest files)들을 담고 있는 GitOps Repository
```

# OKD CI/CD 프로세스
```
1. Source Repo에 변경사항이 Commit
2. Jenkins에서 변경사항을 감지하고 빌드 수행
3. Docker Image를 dockerhub에 Push
4. GitOps Repo의 deployment manifest파일을 업데이트(tag version)
5. ArgoCD가 변경사항을 감지하고 자동 배포 수행
```

# 사전 준비
```
- GitHub repository
- Deploy Key
- dockerhub 계정 및 Repositiry
- okd 계정
```

# 일회성 인스턴스 사용
```
프로젝트용 일회성 Jenkins와 ArgoCD 인스턴스를 사용하는 이유
- 다중 사용자의 경우 관리하기 어렵다. 
- 여러 플러그인 설치로 인해 충돌 가능성이 높다. 
```

# URL References
[Blackwhale OKD](https://console-openshift-console.apps.blackwhale.cloud.hancom.com)  
[ArgoCD](https://argocd-sample-server-okd-tutorial.apps.blackwhale.cloud.hancom.com/)  
[GitHub Source](https://github.com/bluewhale-users/okd-tutorial1-src)  
[GitHub Gitops](https://github.com/bluewhale-users/okd-tutorial1-gitops)  
[DockerHub](https://hub.docker.com/)  
[Test App](http://blog-frontend-okd-tutorial.apps.blackwhale.cloud.hancom.com/)

