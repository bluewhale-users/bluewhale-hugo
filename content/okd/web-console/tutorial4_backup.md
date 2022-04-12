---
title: "Tutorial4_backup"
date: 2022-04-12T09:43:46+09:00
draft: true
---


## NodeJs + React Sample

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