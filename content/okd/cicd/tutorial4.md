---
title: "Tutorial4 : Jenkins 설정"
date: 2022-03-15T11:31:43+09:00
weight: 44
---

## Jenkins 설치


### 1. OKD에 로그인
- [okd link](https://console-openshift-console.apps.blackwhale.cloud.hancom.com/)
{{< figure src="/cicd/tutorial4_1.jpg" title="[접속 화면]" >}}

### 2. Project 만들기  
{{< figure src="/cicd/tutorial4_2.jpg" >}}
{{< figure src="/cicd/tutorial4_3.jpg" title="[프로젝트 생성 화면]" >}}

### 3. 역할 전환(developer)
좌측 상단의 역할선택 드롭메뉴에서 developer을 선택합니다.  
{{< figure src="/cicd/tutorial4_4.jpg#floatleft" >}}
{{< figure src="/cicd/tutorial4_5.jpg" >}}

### 4. Jenkins 설치
```
OKD->Developer->Add
```

#### 4.1 All services 선택  
{{< figure src="/cicd/tutorial4_6.jpg" >}}

#### 4.2 jenkins 로 검색    
{{< figure src="/cicd/tutorial4_7.jpg" >}}

#### 4.3 Jenkins v0.0.3 Helm Charts 버전 설치 (기본 설정 사용)
{{< figure src="/cicd/tutorial4_8.jpg" >}}
{{< figure src="/cicd/tutorial4_9.jpg" >}}

#### 4.4 설치 완료(Pods의 상태가 Running으로 바뀔때까지 대기)
{{< figure src="/cicd/tutorial4_10.jpg" >}}

### 5. OpenURL 아이콘을 선택해 jenkins 서비스 접속
{{< figure src="/cicd/tutorial4_11.jpg" >}}

### 6. Allow selected permissions 선택
{{< figure src="/cicd/tutorial4_12.jpg" >}}

### 7. 접속 완료 화면
{{< figure src="/cicd/tutorial4_13.jpg" >}}