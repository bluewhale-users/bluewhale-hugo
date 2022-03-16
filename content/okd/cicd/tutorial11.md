---
title: "Tutorial11 : 문제 해결"
date: 2022-03-15T11:33:03+09:00
weight: 51
---

## 문제 해결

### 1. OKD BuildConfig 빌드 확인
```
- okd -> Developer -> Builds 
- 생성한 BuildConfig를 선택해 Builds 탭으로 이동하면 빌드 히스토리를 확인할 수 있다.  
```
{{< figure src="/cicd/tutorial11_1.jpg" >}}

### 2. 새로 배포한 버전이 이전 이미지를 참고하는 문제
```
Deployment의 imagePullPolicy가 Always로 주었음에도
이미지 갱신이 되지 않는 경우가 발생한다. 

저장소의 이미지와 로컬에 있는 이미지가 동일한 경우 이런 문제가 발생한다. 

Tag와 Digest 값이 동일한지 확인해본다. 

<before>
spcsenti2023/okdtutorial:latest
DIGEST:sha256:7521223d8a7c54a6c9e5a40b4f4866f4394eefb3494c5de8f47fbf4e536c40e9

<current>
spcsenti2023/okdtutorial:latest
DIGEST:sha256:14480c323c64dd065fa0b71067226ab8995c5f2660a8e7d747795ebc2647e1b8
```

[BuildConfig에서 빌드 번호 자동 업데이트 가능할까?](https://stackoverflow.com/questions/61057627/dynamic-tag-based-on-build-number-in-openshift-buildconfig)
```
[Asked]
I am doing CI/CD using openshift buildconfig. I am able to fetch the source code from git and successfully build the docker image and push to internal registry. I want to tag the image built with with build numbers based on Openshift Build config output labels are annotations. How to do that in the YAML, I am using docker build strategy.

output:
    to:
      kind: DockerImage
      name: 'internal.registry.com/app_name/sample_app:<BUILD_NUMBER/NAME>'
      
Also once this is done, i want to update the image in deployment to get new version of app. Have anyone done such setup, Can anyone help me on this.

[Answer]
The yaml file is resolved when the buildConfig is created, it can't have references to environment variables or build number information. If you are doing this from a CI/CD pipeline, you could create a different buildConfig in the same CI/CD pipeline, run it, and delete it. But you may have permissions issue to create the buildConfig every time.

Another option I would prefer is to use ImageStreams. With ImageStream a single object keeps track of all versions of the image via sha codes, therefore there is no need to update the yaml every time.
```

### 3. https 지원
```
[service.yaml]
....
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 8080
    - name: https
      protocol: TCP
      port: 443
      targetPort: 8080
....

[route.yaml]
spec:
....
 port:
    targetPort: https
....
```