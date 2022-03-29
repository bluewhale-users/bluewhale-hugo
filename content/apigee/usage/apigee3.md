---
title: "Apigee3 : API Reverse Proxy"
date: 2022-03-29T13:44:51+09:00
draft: false
weight: 43
---

### 1. Create New 선택
{{< figure src="/apigee/apigee-tutorial1_1.jpg" >}}

### 2. Reverse proxy 선택
{{< figure src="/apigee/apigee-tutorial1_2.jpg" >}}

### 3. Proxy 설정 추가
```
Name : okd
Target : http://dotnetexample-okd-tutorial.apps.blackwhale.cloud.hancom.com/WeatherForecast
```
{{< figure src="/apigee/apigee-tutorial1_3.jpg" >}}

### 4. Add CORS Headers 체크
{{< figure src="/apigee/apigee-tutorial1_4.jpg" >}}

### 5. Optional Deployment - eval 체크 안함
{{< figure src="/apigee/apigee-tutorial1_5.jpg" >}}

### 6. Create 완료 - Edit proxy 선택
{{< figure src="/apigee/apigee-tutorial1_6.jpg" >}}

### 7. Revision을 1번을 Deploy 한다. 
{{< figure src="/apigee/apigee-tutorial1_7.jpg" >}}

### 8. 서비스 어카운트 설정은 기본값으로 Deploy
{{< figure src="/apigee/apigee-tutorial1_8.jpg" >}}

### 9. URL에 접속해 프록시가 동작하는지 확인한다. 
- https://spsenti2023.duckdns.org/okd

{{< figure src="/apigee/apigee-tutorial1_9.jpg" >}}

### 10. 새버전 추가
{{< figure src="/apigee/apigee-tutorial1_10.jpg" >}}

- 좌측의 Revision Dropdown 메뉴를 선택해 Save as new revision을 선택한다. 
- {{< figure src="/apigee/apigee-tutorial1_11.jpg" >}}

- 새로운 Revision이 생성된다. (수정후 저장)

{{< figure src="/apigee/apigee-tutorial1_12.jpg" >}}

- Overview 탭으로 이동후 새로운 Revision을 선택후 Deploy한다. 

{{< figure src="/apigee/apigee-tutorial1_13.jpg" >}}
{{< figure src="/apigee/apigee-tutorial1_14.jpg" >}}