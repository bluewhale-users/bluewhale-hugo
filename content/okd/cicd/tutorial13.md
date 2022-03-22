---
title: "Tutorial13 : BuildConfig 사용 예"
date: 2022-03-15T11:33:27+09:00
weight: 53
---

## orca-harbor + buildconfig

### 1. image pull secret 추가
{{% notice info %}}
Secret name : orca-harbor-secret  
Registry server address : orca-harbor.cloud.hancom.com  
Username : "이름"  
Password : harbor 접속후 CLI secret 확인  
{{% /notice %}}

{{< figure src="/cicd/tutorial13_1.jpg" >}}

### 2. User Profile을 눌러 CLI secret 복사후 사용
{{< figure src="/cicd/tutorial13_2.jpg" >}}


### 3. BuildConfig 사용 예제1
``` bash
apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: testblog
  namespace: okd-tutorial
  labels:
    app.kubernetes.io/name: testblog  
spec:
  nodeSelector: null
  output:
    to:
      kind: DockerImage
      name: 'image 경로'
    pushSecret:
      name: 'orca-harbor-secret'
  source:
    git:
      ref: master
      uri: 'https://github.com/bluewhale-users/okd-tutorial1-src.git'
    type: Git
  strategy:
    type: Docker
    dockerStrategy:      
      dockerfilePath: Dockerfile
  triggers:
    - type: ImageChange
      imageChange: {}
    - type: ConfigChange
```

### 4. BuildConfig 사용 예제2
``` bash
apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: standardterm
  namespace: okd-externaladdin
  labels:
    app.kubernetes.io/name: standardterm  
spec:
  nodeSelector: null
  output:
    to:
      kind: DockerImage
      name: 'image 경로'
    pushSecret:
      name: 'orca-harbor-usetoken' 
    type: Git
  strategy:
    type: Docker
    dockerStrategy:      
      dockerfilePath: Dockerfile
  postCommit: {}
  source:
    type: Binary
    binary: {}
  runPolicy: Serial
  triggers:
    - type: ImageChange
      imageChange: {}
    - type: ConfigChange
```