---
title: "Tutorial6 : Buildconfig 설정"
date: 2022-03-15T11:32:10+09:00
weight: 46
---

## OKD Buildconfig 설정

```
설치한 Jenkins 버전에는 docker를 포함하지 않는다. 
docker image 빌드를 위해 okd buildconfig를 사용한다. 
```

### 1. BuildConfig 생성
```
- okd -> Developer -> Builds
```

{{< figure src="/cicd/tutorial6_1.jpg" >}}

#### 1.1 Create BuildConfig 선택
{{< figure src="/cicd/tutorial6_2.jpg" >}}

[Jenkinsfile 확인](https://github.com/bluewhale-users/okd-tutorial1-src/blob/master/Jenkinsfile)
```
BuildConfig 이름을 jenkinsfile에 appName 으로 맵핑된다. 

- jenkinsfile의 appName을 BuildConfig의 이름으로 변경한다. 
appName = "okd-tutorial"
```

#### 1.2 아래 내용을 편집해 본인 설정에 맞게 변경한다. 
[BuildConfig YAML 샘플](https://github.com/bluewhale-users/okd-tutorial1-src/blob/master/openshift-build-example.yml)

``` bash
kind: BuildConfig
apiVersion: build.openshift.io/v1
metadata:
  name: okd-tutorial
  labels:
    app.kubernetes.io/name: okd-tutorial
spec:
  nodeSelector: null
  output:
    to:
      kind: DockerImage
      name: 'docker.io/spcsenti2023/okdtutorial:latest'
  strategy:
    type: Docker
    dockerStrategy:      
      dockerfilePath: Dockerfile
  postCommit: {}
  source:
    type: Binary
    binary: {}
  runPolicy: Serial 
```

#### 1.3 생성 화면
{{< figure src="/cicd/tutorial6_3.jpg" >}}

### 2. Secrets 추가
{{< figure src="/cicd/tutorial6_4.jpg" >}}

#### 2.1 Create(Image pull secret) 선택
{{< figure src="/cicd/tutorial6_5.jpg" >}}

#### 2.2 dockerhub에 가입한 아이디와 패스워드를 입력한다. 
```
Secret name : dockerio-okdtutorial
```
{{< figure src="/cicd/tutorial6_6.jpg" >}}

### 3. ServiceAccount(builder)에 secret 추가
```
- okd -> Administrator -> User Management -> ServiceAccounts 이동
```
{{< figure src="/cicd/tutorial6_7.jpg" >}}

#### 4. builder 선택
{{< figure src="/cicd/tutorial6_8.jpg" >}}

#### 5. Secrets 섹션에 dockerio-okdtutorial 추가후 Save 선택
{{< figure src="/cicd/tutorial6_9.jpg" >}}