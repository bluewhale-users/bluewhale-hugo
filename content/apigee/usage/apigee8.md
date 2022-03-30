---
title: "Apigee8 : VS Code에서 Apigee를 사용해 API 프록시 빌드하기"
date: 2022-03-29T13:45:07+09:00
draft: false
weight: 48
---

### 작업 순서
1. Apigee 작업공간을 만들어 Apigee를 사용하는 로컬 개발에 필요한 디렉터리 구조를 설정합니다.
2. API 프록시를 만듭니다. API 프록시를 모의 대상 엔드포인트에 연결하여 작동 방식을 확인할 수 있습니다.
3. 새 API 프록시가 포함된 환경을 구성하고 배포합니다.
4. API를 테스트합니다. 테스트 리소스를 빌드하고 내보내고 API를 테스트하기 위해 API 키를 사용하여 인증하는 방법을 알아봅니다.
5. API 프록시에서 XML 데이터를 반환하도록 대상 엔드포인트를 변경합니다.
6. 정책을 연결하여 응답을 XML에서 JSON으로 변환합니다.
7. Apigee 환경에 배포합니다.
8. 보관 파일을 프로덕션으로 승격합니다.


## Apigee 작업 공간 만들기

### 1. Extention 설치
- Apigee 검색후 Cloud Code 설치   
{{< figure src="/apigee/apigee-tutorial6_1.jpg" >}}

### 2. Cloud Code - Apigee 클릭
{{< figure src="/apigee/apigee-tutorial6_2.jpg" >}}

### 3. Apigee 작업공간 만들기
- Create Apigee workspace 선택  
{{< figure src="/apigee/apigee-tutorial6_3.jpg" >}}

### 4. 이름을 입력후 엔터(myapigeeworkspace)
{{< figure src="/apigee/apigee-tutorial6_4.jpg" >}}

### 5. Explorer 확인
{{< figure src="/apigee/apigee-tutorial6_5.jpg" >}}

---
## API 프록시 만들기

### 1. Apigee 탐색기로 이동
- apiproxies 폴더위에 커서를 놓고 +를 클릭하면 프록시 만들기 마법사가 열립니다.
{{< figure src="/apigee/apigee-tutorial6_6.jpg" >}}

### 2. 역방향 프록시(Reverse proxy)를 선택
- API 키 기반 인증 선택
{{< figure src="/apigee/apigee-tutorial6_7.jpg" >}}


### 3. 프롬프트에 다음 값 입력
입력		                     | 값			               | 설명
:------	                        |:-------			           |:------          
Backend target URL          | https://mocktarget.apigee.net	 | Apigee가 API 프록시에 대한 요청에서 호출하는 대상 URL입니다. mocktarget 서비스는 Apigee에서 호스팅되며 간단한 데이터를 반환합니다.
API proxy name                         | helloworld			 | API 프록시를 식별하는 데 사용되는 이름입니다.
API proxy base path            | helloworld	   | API에 요청을 보내는 데 사용되는 URL의 일부입니다. Apigee는 URL을 사용하여 수신 요청을 적절한 API 프록시로 일치시키며 라우팅합니다.

{{< figure src="/apigee/apigee-tutorial6_8.jpg" >}}
{{< figure src="/apigee/apigee-tutorial6_9.jpg" >}}
{{< figure src="/apigee/apigee-tutorial6_10.jpg" >}}

### 4. 프록시 생성 확인
{{< figure src="/apigee/apigee-tutorial6_11.jpg" >}}

---

## 환경 구성 및 배포
### 1. 환경 생성
- environments의 +버튼 클릭(환경이름 : dev)
{{< figure src="/apigee/apigee-tutorial6_12.jpg" >}}

- dev 환경 확인
{{< figure src="/apigee/apigee-tutorial6_13.jpg" >}}

- deployments.json 편집
{{< figure src="/apigee/apigee-tutorial6_14.jpg" >}}

```
{
  "proxies" : [
    "helloworld"
  ],
  "sharedflows" : []
}
```

### 2. Apigee 에뮬레이터를 설치
- EMULATORS 이동해 우측 구름 아이콘 클릭(이름입력 : apigee-emulator)
{{< figure src="/apigee/apigee-tutorial6_15.jpg" >}}

- 제어포트 선택(8080)
{{< figure src="/apigee/apigee-tutorial6_16.jpg" >}}

- 트래픽 포트 선택(8998)
{{< figure src="/apigee/apigee-tutorial6_17.jpg" >}}

- 완료 화면
{{< figure src="/apigee/apigee-tutorial6_18.jpg" >}}

```
$ docker ps
CONTAINER ID   IMAGE                                                COMMAND               
   CREATED          STATUS          PORTS                                                 
                                        NAMES
a8eb5f815a8f   gcr.io/apigee-release/hybrid/apigee-emulator:1.6.1   "/usr/bin/dumb-init …"   34 minutes ago   Up 33 minutes   7000-7001/tcp, 0.0.0.0:8080->8080/tcp, 7199/tcp, 9042/tcp, 9160/tcp, 0.0.0.0:8998->8998/tcp   apigee-emulator
```

### 3. dev환경 폴더의 우측 지구본 아이콘 클릭
{{< figure src="/apigee/apigee-tutorial6_19.jpg" >}}

- 출력탭 확인  
{{< figure src="/apigee/apigee-tutorial6_20.jpg" >}}

---

## API 테스트

### 1. 터미널탭에서 curl 호출
```
$ curl localhost:8998/helloworld
{"fault":{"faultstring":"Failed to resolve API Key variable request.queryparam.apikey","detail":{"errorcode":"steps.oauth.v2.FailedToResolveAPIKey"}}}

API 키 기반인증 사용 설정으로 인한 오류 메시지 표시됨
apikey 쿼리 매개변수를 사용하여 API 키를 전달해야 한다. 

API 키를 얻으려면 테스트 번들을 만들고 다음 테스트 리소스를 구성해야 합니다.
- API 제품: API를 번들로 만들고 개발자에게 제공하는 데 사용합니다.
- 개발자: API에 액세스할 앱을 만듭니다.
- 개발자 앱: API 키를 사용하여 API에 액세스할 수 있도록 설정합니다.
```

### 2. 테스트 번들 만들기
- 테스트 폴더의 +버튼을 눌러 추가(이름 : mytestbundle)
{{< figure src="/apigee/apigee-tutorial6_21.jpg" >}}

- products.json 파일 우측의 +클릭(제품이름 : myproduct)
{{< figure src="/apigee/apigee-tutorial6_22.jpg" >}}

- 설명 입력
{{< figure src="/apigee/apigee-tutorial6_23.jpg" >}}

- helloworld 선택
{{< figure src="/apigee/apigee-tutorial6_24.jpg" >}}

> products.json
```
[
  {
    "attributes": [
      {
        "name": "sample_attribute_0",
        "value": "sample_attribute_value_0"
      }
    ],
    "scopes": [],
    "environments": [],
    "apiResources": [
      "/",
      "/*",
      "/**"
    ],
    "quota": "100",
    "quotaInterval": "1",
    "quotaTimeUnit": "minute",
    "name": "myproduct",
    "displayName": "myproduct",
    "proxies": [
      "helloworld"
    ]
  }
]
```

### 3. 개발자 테스트 리소스 구성
- developers.json파일 우측의 "+" 클릭(이메일 입력)
{{< figure src="/apigee/apigee-tutorial6_24.jpg" >}}
{{< figure src="/apigee/apigee-tutorial6_26.jpg" >}}
{{< figure src="/apigee/apigee-tutorial6_27.jpg" >}}
{{< figure src="/apigee/apigee-tutorial6_28.jpg" >}}

```
개발자 이메일: hskim@XXXX.com
사용자 이름: hskim  
이름: haksoo
성: kim
```

> developers.json
```
[
  {
    "attributes": [
      {
        "name": "sample_attribute_0",
        "value": "sample_attribute_value_0"
      }
    ],
    "email": "hskim@XXXX.com",
    "userName": "hskim",
    "firstName": "haksoo",
    "lastName": "kim"
  }
]
```

### 4. 개발자 앱 테스트 리소스 구성
- developerapps.json파일 우측의 +클릭(사용자 등록 이메일 선택)
{{< figure src="/apigee/apigee-tutorial6_29.jpg" >}}

- myapp 입력
{{< figure src="/apigee/apigee-tutorial6_30.jpg" >}}

- myapp 입력
{{< figure src="/apigee/apigee-tutorial6_31.jpg" >}}

- callback url 비워놓기
{{< figure src="/apigee/apigee-tutorial6_32.jpg" >}}

- myproduct 선택
{{< figure src="/apigee/apigee-tutorial6_33.jpg" >}}

```
앱 소유자 hskim@XXXX.com
앱 이름: myapp
설명: myapp
콜백 URL: 비워 둠
만료값 : 사용안함
```

>developerapps.json
```
[
  {
    "attributes": [
      {
        "name": "sample_attribute_0",
        "value": "sample_attribute_value_0"
      }
    ],
    "developerEmail": "hskim@hancom.com",
    "name": "myapp",
    "displayName": "myapp",
    "callbackUrl": "",
    "apiProducts": [
      "myproduct"
    ],
    "expiryType": "never"
  }
]
```

### 5. Apigee 에뮬레이터로 테스트 리소스 내보내기
- mytestbundle 우측의 내보내기 버튼 클릭
{{< figure src="/apigee/apigee-tutorial6_35.jpg" >}}

- Active test data에 표시
{{< figure src="/apigee/apigee-tutorial6_36.jpg" >}}

- 에뮬레이터 탭의 Active developer apps 확인(consumerKey가 등록되어 있다.)
{{< figure src="/apigee/apigee-tutorial6_37.jpg" >}}

- apikey 확인
```
"consumerKey": "ecQEvhRpieEjz75KArOP1U66GGXkoQqN",
```

- curl 호출하여 응답 확인
```
$ curl localhost:8998/helloworld?apikey=ecQEvhRpieEjz75KArOP1U66GGXkoQqN
Hello, Guest!
```

---

## 대상 엔드포인트 변경
- helloworld API 프록시 번들을 펼치고 targets 폴더에서 default.xml을 클릭하여 편집
{{< figure src="/apigee/apigee-tutorial6_38.jpg" >}}

```
<TargetEndpoint name="default">
	<HTTPTargetConnection>
		<URL>https://mocktarget.apigee.net</URL>
	</HTTPTargetConnection>
</TargetEndpoint>
```

> URL 변경
```
<TargetEndpoint name="default">
	<HTTPTargetConnection>
		<URL>https://mocktarget.apigee.net/xml</URL>
	</HTTPTargetConnection>
</TargetEndpoint>
```

- 저장후 dev 환경 폴더의 배포 아이콘을 클릭
{{< figure src="/apigee/apigee-tutorial6_39.jpg" >}}

- Deploy without a test bundle 선택후 배포
{{< figure src="/apigee/apigee-tutorial6_40.jpg" >}}

- curl 실행 결과
```
$ curl localhost:8998/helloworld?apikey=EdKgpEh5jSN9cxlAdfaL2uBYorINbTKE
<?xml version="1.0" encoding="UTF-8"?> <root><city>San Jose</city><firstName>John</firstName><lastName>Doe</lastName><state>CA</state></root>
```

---

## 정책 연결

> 정책은 메시지 형식 변환, 액세스 제어 적용, 원격 서비스 호출, 사용자 승인, 메시지 콘텐츠에서 잠재적 위협 검사 이상의 작업을 수행할 수 있습니다.

### 1. 새 정책을 만들고 PreFlow 응답 흐름의 API 프록시에 연결하여 다른 처리가 실행되기 전에 정책이 적용되도록 합니다.
- XMLtoJSON 정책을 만든다. (polocies폴더의 +버튼을 클릭한다.)
{{< figure src="/apigee/apigee-tutorial6_41.jpg" >}}

- 미디에이션을 선택
{{< figure src="/apigee/apigee-tutorial6_42.jpg" >}}

- XML to JSON 정책 유형 선택
{{< figure src="/apigee/apigee-tutorial6_43.jpg" >}}

- 정책이름(XMLtoJSON) 입력
{{< figure src="/apigee/apigee-tutorial6_44.jpg" >}}

- XMLtoJSON.xml파일이 추가된 화면
{{< figure src="/apigee/apigee-tutorial6_45.jpg" >}}

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<XMLToJSON async="false" continueOnError="false" enabled="true" name="XMLtoJSON">
    <DisplayName>XMLtoJSON</DisplayName>
    <Properties/>
    <Format>yahoo</Format>
    <OutputVariable>request</OutputVariable>
    <Source>request</Source>
</XMLToJSON>
```

> OutputVariable 및 Source 요소 변경
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<XMLToJSON async="false" continueOnError="false" enabled="true" name="XMLtoJSON">
    <DisplayName>XMLtoJSON</DisplayName>
    <Properties/>
    <Format>yahoo</Format>
    <OutputVariable>response</OutputVariable>
    <Source>response</Source>
</XMLToJSON>
```

### 2. 정책을 기본 프록시 엔드포인트에 연결
- helloworld API 프록시 번들의 프록시 폴더를 열고 default.xml을 편집
```
<ProxyEndpoint name="default">
	<PreFlow name="PreFlow">
		<Request>
			<Step>
				<Name>verify-api-key</Name>
			</Step>
			<Step>
				<Name>remove-query-param-apikey</Name>
			</Step>
			<Step>
				<Name>impose-quota</Name>
			</Step>
		</Request>
	</PreFlow>
	<HTTPProxyConnection>
		<BasePath>/helloworld</BasePath>
	</HTTPProxyConnection>
	<RouteRule name="default-route">
		<TargetEndpoint>default</TargetEndpoint>
	</RouteRule>
</ProxyEndpoint>
```

- 아래와 같이 Response 요소를 추가
```
<ProxyEndpoint name="default">
   <PreFlow name="PreFlow">
      <Request>
         <Step>
            <Name>verify-api-key</Name>
         </Step>
         <Step>
            <Name>remove-query-param-apikey</Name>
         </Step>
         <Step>
            <Name>impose-quota</Name>
         </Step>
      </Request>
      <Response>
         <Step>
            <Name>XMLtoJSON</Name>
         </Step>
      </Response>
   </PreFlow>
 ...
</ProxyEndpoint>
```

- dev환경의 배포 아이콘을 클릭(Deploy without a test bundle 선택)
{{< figure src="/apigee/apigee-tutorial6_46.jpg" >}}

- curl 수행(XML응답이 다음과 같이 JSON으로 변환된다.)
```
$ curl localhost:8998/helloworld?apikey=EdKgpEh5jSN9cxlAdfaL2uBYorINbTKE
{"root":{"city":"San Jose","firstName":"John","lastName":"Doe","state":"CA"}
```

