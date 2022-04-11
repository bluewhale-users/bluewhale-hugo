---
title: "Tutorial4 : 사용자 Git 리파지터리 소스로부터 애플리케이션 배포해보기"
date: 2022-04-11T09:50:05+09:00
draft: false
weight: 44
---

[Sample Github](https://github.com/bluewhale-users/okd-tutorial2-src)

## 1. 프로젝트에 추가 
- 우클릭하여 'Add to Project -> From Git' 선택
{{< figure src="/web-console/tutorial4_1.jpg" >}}

Sample Git Repo
```
https://github.com/bluewhale-users/okd-tutorial2-src
```

- Git Repo URL에 Sample URL을 입력한다. 
{{< figure src="/web-console/tutorial4_9.jpg" >}}

{{% notice info %}}
URL 입력후 하단에 'Validated' 메시지가 보인다면 연결이 가능한 상태이다.  
소스 리파티터리 분석후 빌드 이미지를 자동 검출한다. 
(샘플의 경우 Node.js)
{{% /notice %}}


- 아래로 스크롤해 Application name과 Name을 입력후 Create 버튼을 누른다. (다른 옵션은 기본값 사용)
```
Builder Image version : 14-ubi7
Application name : okd-tutorial-2-src-app
Name : okd-tutorial-1-src
Resources : Deployment
Create a route to the Applicaiton : Checked
```

- Advanced options의 "Show advanced Routing options"을 확장해 Target port를 "3000"으로 변경한다. 
{{< figure src="/web-console/tutorial4_10.jpg" >}}

- Build가 끝날때까지 기다린다.
{{< figure src="/web-console/tutorial4_11.jpg" >}}

- Build 성공(Open URL을 눌러 접속 확인)
{{< figure src="/web-console/tutorial4_12.jpg" >}}

- 접속 화면
{{< figure src="/web-console/tutorial4_13.jpg" >}}

---

[Sample Github](https://github.com/bluewhale-users/okd-tutorial1-src)

## 1. 프로젝트에 추가 
- 우클릭하여 'Add to Project -> From Git' 선택
{{< figure src="/web-console/tutorial4_1.jpg" >}}

Sample Git Repo
```
https://github.com/bluewhale-users/okd-tutorial1-src
```

- Git Repo URL에 Sample URL을 입력한다. 
{{< figure src="/web-console/tutorial4_2.jpg" >}}

- 아래로 스크롤해 Application name과 Name을 입력후 Create 버튼을 누른다. (다른 옵션은 기본값 사용)
{{< figure src="/web-console/tutorial4_3.jpg" >}}

```
Application name : okd-tutorial-1-src-app
Name : okd-tutorial-1-src
Resources : Deployment
Create a route to the Applicaiton : Checked
```

- Build가 끝날때까지 기다린다.
{{< figure src="/web-console/tutorial4_4.jpg" >}}

- 빌드 오류
{{< figure src="/web-console/tutorial4_5.jpg" >}}

- View Logs를 선택해 오류내용을 확인한다. 
```
......
npm WARN tar ENOENT: no such file or directory, open '/opt/app-root/src/node_modules/.staging/es5-ext-56afdd2c/test/array/#/fill/shim.js'
npm WARN tar ENOENT: no such file or directory, open '/opt/app-root/src/node_modules/.staging/es5-ext-56afdd2c/test/array/#/filter/shim.js'
npm ERR! code ECONNRESET
npm ERR! errno ECONNRESET
npm ERR! network request to https://registry.npmjs.org/obuf/-/obuf-1.1.2.tgz failed, reason: Client network socket disconnected before secure TLS connection was established
npm ERR! network This is a problem related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'
......
npm ERR! A complete log of this run can be found in:
npm ERR!     /opt/app-root/src/.npm/_logs/2022-04-11T02_01_56_197Z-debug.log
error: build error: error building at STEP "RUN /usr/libexec/s2i/assemble": error while running runtime: exit status 1
```

- 'Edit okd-tutorial-1.src'를 선택하여 수정
{{< figure src="/web-console/tutorial4_6.jpg" >}}

- Build Image version을 최신버전으로 변경후 Save를 선택한다. 
{{< figure src="/web-console/tutorial4_7.jpg" >}}

- 다시 빌드가 끝날때까지 기다린다. 
{{< figure src="/web-console/tutorial4_8.jpg" >}}