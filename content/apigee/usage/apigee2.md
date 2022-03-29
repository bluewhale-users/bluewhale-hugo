---
title: "Apigee2 : 무료로 사용해보기"
date: 2022-03-29T13:44:49+09:00
draft: false
weight: 42
---


### 1. [Apigee](https://cloud.google.com/apigee) 이동

### 2. 무료로 사용해 보기 선택
{{< figure src="/apigee/install_1.jpg" >}}

### 3. GCP project ID가 필요하다. 
{{< figure src="/apigee/install_2.jpg" >}}

{{% notice info %}}
프로젝트는 모든 Google Cloud 리소스를 구성합니다. 프로젝트는 사용자 집합, API 집합, 그리고 이러한 API에 대한 청구, 인증, 모니터링 설정으로 구성됩니다. 예를 들어 모든 Cloud Storage 버킷과 객체는 이를 액세스할 수 있는 사용자 권한과 함께 프로젝트에 상주합니다. 프로젝트를 한 개만 갖거나 여러 프로젝트를 만들 수 있으며, 이를 사용하여 Cloud Storage 데이터를 포함한 Google Cloud 리소스를 논리적 그룹으로 구성할 수 있습니다.
{{% /notice %}}

### 4. [GCP](https://console.cloud.google.com/projectcreate?pli=1) 이동

상단의 팝업 메시지 "자세히 알아보기" 선택
{{% notice info %}}
$300 크레딧으로 무료 체험판을 시작해 보세요. 크레딧을 모두 사용해도 요금이 청구되지 않으니 걱정하지 마세요.
{{% /notice %}}

[무료로 시작하기](https://cloud.google.com/free?_ga=2.209616023.-421691564.1643086771)
{{< figure src="/apigee/install_3.jpg" >}}

### 5. 무료로 시작하기 선택
{{< figure src="/apigee/install_5.jpg" >}}

### 6. 1단계 정보 입력
{{< figure src="/apigee/install_6.jpg" >}}

### 7. 2단계 정보 확인
{{< figure src="/apigee/install_7.jpg" >}}

### 8. 3단계 정보 확인
{{< figure src="/apigee/install_8.jpg" >}}

### 9. 3단계 정보 확인(결제 정보 확인)
{{< figure src="/apigee/install_9.jpg" >}}

### 10. 설문조사
{{< figure src="/apigee/install_10.jpg" >}}

### 11. 홈 -> 대시보드 선택
{{< figure src="/apigee/install_11.jpg" >}}

### 12. Project ID 확인
```
프로젝트 이름
My First Project
프로젝트 번호
432606567641
프로젝트 ID
pure-fold-339305
```
{{< figure src="/apigee/install_12.jpg" >}}

### 13. Apigee 설정 화면 -> Project ID 입력후 START EVALUATION 선택
{{< figure src="/apigee/install_13.jpg" >}}

### 14. API 사용 설정(연필아이콘 선택)
{{< figure src="/apigee/install_14.jpg" >}}

### 15. Networking 설정후 ALLOCATE AND CONNECT 선택
```
Authorized network : default
Reserve Peering Ranges : Automatically allocate IP range
```
{{< figure src="/apigee/install_15.jpg" >}}

### 16. Apigee evaluation organization 설정후 Provision 선택
```
Analytics hosting region : asia-east1
Runtime location : asia-east1

프로비저닝하는데 시간이 40~50분정도 걸린다.
```
{{< figure src="/apigee/install_16.jpg" >}}

### 17. Access routing 설정
- Domain 입력을 해야 한다. 
{{< figure src="/apigee/install_17.jpg" >}}

{{% notice info %}}
Domain이 없기 때문에 무료 도메인을 하나 생성한다. 
{{% /notice %}}

### 18. 무료도메인 신청
- [Duck DNS](https://www.duckdns.org/)
{{< figure src="/apigee/install_19.jpg" >}}

### 19. 생성하고자 하는 도메인 이름을 서브 도메인에 입력한다.  
{{< figure src="/apigee/install_20.jpg" >}}

### 20. ip 주소를 업데이트한다. 
```
현재 External-ip를 모르니까.. 설정 완료후 출력되는 ip 주소를 입력한다. 
```

### 21. Apigee 설정에서 발급받은 도메인을 등록한다. 
{{< figure src="/apigee/install_21.jpg" >}}

### 22. 설정완료
{{< figure src="/apigee/install_22.jpg" >}}

### 23. External-IP를 Duck DNS에서 업데이트 한다. 
```
Configure DNS
Create an A record that points spsenti2023.duckdns.org to 34.117.255.14
Test your Apigee runtime end to end
Launch spsenti2023.duckdns.org to test the 'Hello world' API.
```
{{< figure src="/apigee/install_23.jpg" >}}

### 24. Launch를 눌러 확인해본다. (배포까지 시간이 필요할 수도 있다.)
{{< figure src="/apigee/install_26.jpg" >}}

### 25. HTTPS 접속 문제가 발생할 경우 HTTP 프로토콜을 로드밸런서에 추가한다. 
- GCP Console로 이동한다. 
- 네트워크 서비스 - 부하 분산 을 선택한다. 
{{< figure src="/apigee/install_27.jpg" >}}

- 부하분산기를 선택한다. 
{{< figure src="/apigee/install_28.jpg" >}}

- 수정을 선택한다. 
{{< figure src="/apigee/install_29.jpg" >}}

- 프런트엔드 구성을 선택하여 IP 및 포트 추가를 선택한다. 
{{< figure src="/apigee/install_24.jpg" >}}

- HTTP/80 포트를 추가한다. 
{{< figure src="/apigee/install_25.jpg" >}}

### 26. 로드밸런서 수정후 다시 접속해 확인한다. 

https://spsenti2023.duckdns.org/hello-world
{{< figure src="/apigee/install_30.jpg" >}}
