---
title: "Tutorial9"
date: 2022-03-15T11:32:43+09:00
weight: 49
---

# ArgoCD App 배포하기

## 1. image registry 주소 변경
[GitOps Repo](https://github.com/blackwhale-testuser/okd-tutorial1-gitops)


```
아래 2개의 yaml파일을 편집해 이미지 경로를 본인 dockerhub의 계정과 리파지토리로 변경한다. 
base/deployment-sample.yaml  
okd-deploy/testblog-deployment.yaml

image: docker.io/spcsenti/testblog:latest --> image: docker.io/spcsenti2023/okdtutorial:latest
```

## 2. New App 선택
```
[GENERAL]
Application Name : okd-tutorial
Project : default

[SOURCE]
Repository URL : https://github.com/blackwhale-testuser/okd-tutorial1-gitops
Revision : HEAD
Path : okd-deploy

[DESTINATION]
Cluster URL : https://kubernetes.default.svc
Namespace : okd-tutorial

```
{{< figure src="/cicd/tutorial9_1.jpg" >}}

### Out of Sync일 경우에는 SYNC 버튼을 눌러 Synchronize를 수행한다. 
{{< figure src="/cicd/tutorial9_2.jpg" >}}

### Topology를 확인한다. 
```
blog-frontend가 배포되었는지 확인
```
{{< figure src="/cicd/tutorial9_3.jpg" >}}

### OpenURL을 눌러 확인한다. 
{{< figure src="/cicd/tutorial9_4.jpg" >}}