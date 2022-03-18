---
title: "Tutorial5 : Jenkins Pipeline 구성"
date: 2022-03-15T11:31:56+09:00
weight: 45
---

## Jenkins Pipeline 구성

### 1. ssh agent plug-in 설치
* Jenkins -> Jenkins 관리 -> 플러그인 관리 이동  
* "ssh agent" 검색
  
{{< figure src="/cicd/tutorial5_1.jpg" >}}

#### 1.1 Download now and install after restart 선택
{{< figure src="/cicd/tutorial5_2.jpg" >}}

#### 1.2 설치가 끝나고 실행중인 작업이 없으면 Jenkins 재시작 선택
{{< figure src="/cicd/tutorial5_3.jpg" >}}

#### 1.3 로그인 화면
{{< figure src="/cicd/tutorial5_4.jpg" >}}

### 2. credentials 등록
* Jenkins -> Jenkins 관리 -> Manage Credentials 이동

#### 2.1 (Global) 도메인 선택
{{< figure src="/cicd/tutorial5_5.jpg" >}}

#### 2.2 Add Credentials 선택
{{< figure src="/cicd/tutorial5_6.jpg" >}}

- [Jenkinsfile 확인](https://github.com/bluewhale-users/okd-tutorial1-src/blob/master/Jenkinsfile)

{{% notice info %}}
jenkinsfile의 credentialsId 이름으로 등록한다.  
credentialsId 'jenkins-ssh-private'  
ID : jenkins-ssh-private  
Username : jenkins-ssh-private  
Private Key : 이전단계에서 생성한 Private key를 등록한다.   
{{% /notice %}}

{{< figure src="/cicd/tutorial5_7.jpg" >}}
{{< figure src="/cicd/tutorial5_8.jpg" >}}

### 3. 새로운 아이템 생성
{{< figure src="/cicd/tutorial5_9.jpg" >}}

{{% notice info %}}
item name : okd-turotial  
type : pipeline 선택
{{% /notice %}}

{{< figure src="/cicd/tutorial5_10.jpg" >}}

#### 3.1 General 설정
{{% notice info %}}
GitHub project 체크  
Project url : https://github.com/blackwhale-testuser/okd-tutorial1-src
{{% /notice %}}

{{< figure src="/cicd/tutorial5_11.jpg" >}}

#### 3.2 Build Triggers 설정
{{% notice info %}}
GitHub hook trigger for GITScm polling 체크
{{% /notice %}}

{{< figure src="/cicd/tutorial5_12.jpg" >}}

#### 3.3 Pipeline 설정
{{% notice info %}}
Definition : Pipeline script from SCM 선택  
Repository URL : https://github.com/blackwhale-testuser/okd-tutorial1-src  
Branch Specifier : */master  
{{% /notice %}}

{{< figure src="/cicd/tutorial5_13.jpg" >}}

> SCM(Source Code Management) : git이나 svn과 같은 소스관리 도구