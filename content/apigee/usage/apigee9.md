---
title: "Apigee9 : Apigee 환경에 배포하기"
date: 2022-03-29T13:45:10+09:00
draft: false
weight: 49
---

#### 0. Google Cloud SDK와 gcloud beta apigee 구성요소 설치

- gcloud beta 구성요소 설치
```
gcloud components install beta
```

- 베타 구성요소 설치 확인
```
$ gcloud components list

Your current Google Cloud CLI version is: 373.0.0
The latest available version is: 373.0.0

┌────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                 Components                                                 │
├───────────────┬──────────────────────────────────────────────────────┬──────────────────────────┬──────────┤
│     Status    │                         Name                         │            ID            │   Size   │
├───────────────┼──────────────────────────────────────────────────────┼──────────────────────────┼──────────┤
│ Not Installed │ App Engine Go Extensions                             │ app-engine-go            │  4.2 MiB │
│ Not Installed │ Appctl                                               │ appctl                   │ 18.7 MiB │
│ Not Installed │ Cloud Bigtable Command Line Tool                     │ cbt                      │  8.4 MiB │
│ Not Installed │ Cloud Bigtable Emulator                              │ bigtable                 │  5.9 MiB │
│ Not Installed │ Cloud Datalab Command Line Tool                      │ datalab                  │  < 1 MiB │
│ Not Installed │ Cloud Datastore Emulator                             │ cloud-datastore-emulator │ 18.4 MiB │
│ Not Installed │ Cloud Firestore Emulator                             │ cloud-firestore-emulator │ 40.5 MiB │
│ Not Installed │ Cloud Pub/Sub Emulator                               │ pubsub-emulator          │ 60.7 MiB │
│ Not Installed │ Cloud SQL Proxy                                      │ cloud_sql_proxy          │  7.4 MiB │
│ Not Installed │ Google Container Registry's Docker credential helper │ docker-credential-gcr    │  1.8 MiB │
│ Not Installed │ anthos-auth                                          │ anthos-auth              │ 18.1 MiB │
│ Not Installed │ config-connector                                     │ config-connector         │ 49.7 MiB │
│ Not Installed │ gcloud Alpha Commands                                │ alpha                    │  < 1 MiB │
│ Not Installed │ gcloud app Java Extensions                           │ app-engine-java          │ 51.6 MiB │
│ Not Installed │ gcloud app PHP Extensions                            │ app-engine-php           │ 19.1 MiB │
│ Not Installed │ gcloud app Python Extensions                         │ app-engine-python        │  7.8 MiB │
│ Not Installed │ gcloud app Python Extensions (Extra Libraries)       │ app-engine-python-extras │ 26.4 MiB │
│ Not Installed │ kubectl-oidc                                         │ kubectl-oidc             │ 18.1 MiB │
│ Not Installed │ pkg                                                  │ pkg                      │          │
│ Installed     │ BigQuery Command Line Tool                           │ bq                       │  1.0 MiB │
│ Installed     │ Cloud Storage Command Line Tool                      │ gsutil                   │  8.1 MiB │
│ Installed     │ Google Cloud CLI Core Libraries                      │ core                     │ 22.2 MiB │
│ Installed     │ Minikube                                             │ minikube                 │ 27.3 MiB │
│ Installed     │ Skaffold                                             │ skaffold                 │ 17.8 MiB │
│ Installed     │ gcloud Beta Commands                                 │ beta                     │  < 1 MiB │
│ Installed     │ kubectl                                              │ kubectl                  │  < 1 MiB │
└───────────────┴──────────────────────────────────────────────────────┴──────────────────────────┴──────────┘
To install or remove components at your current SDK version [373.0.0], run:
  $ gcloud components install COMPONENT_ID
  $ gcloud components remove COMPONENT_ID

To update your SDK installation to the latest version [373.0.0], run:
  $ gcloud components update
```

- gcloud에 대한 액세스 권한 승인(Cloud SDK 초기화의 설명에 따라 계정을 인증하고 액세스 권한을 부여하고 Cloud SDK 설치를 초기화합니다.)
```
$ gcloud init
Welcome! This command will take you through the configuration of gcloud.

Your current configuration has been set to: [default]

You can skip diagnostics next time by using the following flag:
  gcloud init --skip-diagnostics

Network diagnostic detects and fixes local network connection issues.
Checking network connection...done.
Reachability Check passed.
Network diagnostic passed (1/1 checks passed).

You must log in to continue. Would you like to log in (Y/n)?  y

Your browser has been opened to visit:

    https://accounts.google.com/o/oauth2/auth?response_type=code&client_id=32555940559.apps.googleusercontent.com&redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&scope=openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&state=EEOOAQ5tPUJqdDcPn3scJTRVd38L4T&access_type=offline&code_challenge=v3xratBRwmNAVE5x1vb25t8q-5PVSvAj4pnbVoFtBTs&code_challenge_method=S256

You are logged in as: [spcsenti2023@gmail.com].

Pick cloud project to use: 
 [1] pure-fold-339305
 [2] Enter a project ID
 [3] Create a new project
Please enter numeric choice or text value (must exactly match list item):  PS D:\Git\apigee\myapigeeworkspace> gcloud init
Please enter a value between 1 and 3, or a value present in the list:  Welcome! This command will take you through the configuration of gcloud.
Please enter a value between 1 and 3, or a value present in the list:
Please enter a value between 1 and 3, or a value present in the list:  Your current configuration has been set to: [default]
Please enter a value between 1 and 3, or a value present in the list:
Please enter a value between 1 and 3, or a value present in the list:  You can skip diagnostics next time by using the following flag:
Please enter a value between 1 and 3, or a value present in the list:    gcloud init --skip-diagnostics
Please enter a value between 1 and 3, or a value present in the list:
Please enter a value between 1 and 3, or a value present in the list:  Network diagnostic detects and fixes local network connection issues.
Please enter a value between 1 and 3, or a value present in the list:  Checking network connection...done.
Please enter a value between 1 and 3, or a value present in the list:  Reachability Check passed.
Please enter a value between 1 and 3, or a value present in the list:  Network diagnostic passed (1/1 checks passed).
Please enter a value between 1 and 3, or a value present in the list:
Please enter a value between 1 and 3, or a value present in the list:  You must log in to continue. Would you like to log in (Y/n)?  y
Please enter a value between 1 and 3, or a value present in the list:  1

Your current project has been set to: [pure-fold-339305].

Do you want to configure a default Compute Region and Zone? (Y/n)?  y

Which Google Compute Engine zone would you like to use as project default?
If you do not specify a zone via a command line flag while working with Compute Engine resources, the default is assumed.
 [1] us-east1-b
 [2] us-east1-c
 [3] us-east1-d
 [4] us-east4-c
 [5] us-east4-b
 [6] us-east4-a
 [7] us-central1-c
 [8] us-central1-a
 [9] us-central1-f
 [10] us-central1-b
 [11] us-west1-b
 [12] us-west1-c
 [13] us-west1-a
 [14] europe-west4-a
 [15] europe-west4-b
 [16] europe-west4-c
 [17] europe-west1-b
 [18] europe-west1-d
 [19] europe-west1-c
 [20] europe-west3-c
 [21] europe-west3-a
 [22] europe-west3-b
 [23] europe-west2-c
 [24] europe-west2-b
 [25] europe-west2-a
 [26] asia-east1-b
 [27] asia-east1-a
 [28] asia-east1-c
 [29] asia-southeast1-b
 [30] asia-southeast1-a
 [31] asia-southeast1-c
 [32] asia-northeast1-b
 [33] asia-northeast1-c
 [34] asia-northeast1-a
 [35] asia-south1-c
 [36] asia-south1-b
 [37] asia-south1-a
 [38] australia-southeast1-b
 [39] australia-southeast1-c
 [40] australia-southeast1-a
 [41] southamerica-east1-b
 [42] southamerica-east1-c
 [43] southamerica-east1-a
 [44] asia-east2-a
 [45] asia-east2-b
 [46] asia-east2-c
 [47] asia-northeast2-a
 [48] asia-northeast2-b
 [49] asia-northeast2-c
 [50] asia-northeast3-a
Did not print [39] options.
Too many options [89]. Enter "list" at prompt to print choices fully.
Please enter numeric choice or text value (must exactly match list item):  27

Your project default Compute Engine zone has been set to [asia-east1-a].
You can change it by running [gcloud config set compute/zone NAME].

Your project default Compute Engine region has been set to [asia-east1].
You can change it by running [gcloud config set compute/region NAME].

Created a default .boto configuration file at [C:\Users\user\.boto]. See this file and
[https://cloud.google.com/storage/docs/gsutil/commands/config] for more
information about configuring Google Cloud Storage.
Your Google Cloud SDK is configured and ready to use!

* Commands that require authentication will use spcsenti2023@gmail.com by default
* Commands will reference project `pure-fold-339305` by default
* Compute Engine commands will use region `asia-east1` by default
* Compute Engine commands will use zone `asia-east1-a` by default

Run `gcloud help config` to learn how to change individual settings

This gcloud configuration is called [default]. You can create additional configurations if you work with multiple accounts and/or projects.
Run `gcloud topic configurations` to learn more.

Some things to try next:

* Run `gcloud --help` to see the Cloud Platform services you can interact with. And run `gcloud help COMMAND` to get help on any gcloud command.
* Run `gcloud topic --help` to learn about advanced features of the SDK like arg files and output formatting
* Run `gcloud cheat-sheet` to see a roster of go-to `gcloud` commands.
```

- 추가 설정을 수행하지 않고 액세스 승인
```
PS D:\Git\apigee\myapigeeworkspace> gcloud auth login
Your browser has been opened to visit:

    https://accounts.google.com/o/oauth2/auth?response_type=code&client_id=32555940559.apps.googleusercontent.com&redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&scope=openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Faccounts.reauth&state=8vekqoeRbLfEc9a1RMdtKuAGKoQsHk&access_type=offline&code_challenge=dKREWjk04tSgbIgnh-vIjtdZI8zYXXafijjRZ4h9OFg&code_challenge_method=S256


You are now logged in as [spcsenti2023@gmail.com].
Your current project is [pure-fold-339305].  You can change this setting by running:
  $ gcloud config set project PROJECT_ID
```

{{< figure src="/apigee/apigee-tutorial7_4.jpg" >}}
{{< figure src="/apigee/apigee-tutorial7_5.jpg" >}}

### 1. Apigee 조직에 새로운 dev 환경을 만들고 배포 유형으로 Archive를 사용 설정합니다.

- Apigee 웹콘솔의 Admin - Environments - Overview 이동(우측 상단의 +Environment 선택)
{{< figure src="/apigee/apigee-tutorial7_1.jpg" >}}

- 이름 dev, 배포유형 Archive를 사용 설정
{{< figure src="/apigee/apigee-tutorial7_2.jpg" >}}

- 새 환경 추가
{{< figure src="/apigee/apigee-tutorial7_3.jpg" >}}

- 인스턴스 연결
{{< figure src="/apigee/apigee-tutorial7_16.jpg" >}}

- dev를 체크하고 save를 선택한다.(몇분 정도 걸린다.)
{{< figure src="/apigee/apigee-tutorial7_17.jpg" >}}

- 연결 완료
{{< figure src="/apigee/apigee-tutorial7_18.jpg" >}}


### 2. 환경 그룹 연결
- Groups에 기존 eval-group을 연결
{{< figure src="/apigee/apigee-tutorial7_19.jpg" >}}

###  3. Apigee 환경에 API 프록시 구성 아카이브 파일을 배포
```
# 터미널탭에서 myapigeeworkspace 디렉토리로 이동
$ cd myapigeeworkspace


# 다음 명령을 실행
gcloud beta apigee archives deploy --environment=dev --labels=release=052021

# 실행 응답
Waiting for operation [0ef6eb0a-b5a6-41fb-9c86-13c1dc0a751c] to complete...done.
```

### 4. API 테스트
```
curl https://INTERNAL_LOAD_BALANCER_IP/helloworld /
  -H "Host: ENV_GROUP_HOSTNAME" 
```

- 다음과 같은 오류 메시지를 확인할 수 있다. 
```
$ curl https://spsenti2023.duckdns.org/helloworld -H "Host: pure-fold-339305-eval.apigee.net" 

{"fault":{"faultstring":"Failed to resolve API Key variable request.queryparam.apikey","detail":{"errorcode":"steps.oauth.v2.FailedToResolveAPIKey"}}}
```

helloworld API를 포함하는 API 제품을 만든 후 API 제품을 사용해 개발자를 만들고 등록해야 API 키를 가져올 수 있다. 

### 5. API 키 가져오기
- Publish - API Products 이동
{{< figure src="/apigee/apigee-tutorial7_20.jpg" >}}

- CREATE를 선택
{{< figure src="/apigee/apigee-tutorial7_21.jpg" >}}

```
Name: myproduct
Display name: myproduct
Environment: dev
Access: public
Quota: 공란
Allowed OAuth scope: 공란
```

- Operations 항목에서 Add an operation을 선택
{{< figure src="/apigee/apigee-tutorial7_22.jpg" >}}

```
- API 프록시 드롭다운 메뉴에서 helloworld 선택
- 경로 필드에 "/" 입력
- 다른 필드는 기본값 그대로 사용
- 저장을 눌러 API 제품을 저장
```
{{< figure src="/apigee/apigee-tutorial7_23.jpg" >}}

- 저장 완료
{{< figure src="/apigee/apigee-tutorial7_24.jpg" >}}


### 6. 개발자 추가
- Publish - Developers로 이동하여 개발자를 등록한다. 
{{< figure src="/apigee/apigee-tutorial7_25.jpg" >}}



### 7. 앱 등록
- Publish -> Apps로 이동하여 +App을 눌러 추가
 {{< figure src="/apigee/apigee-tutorial7_26.jpg" >}}

 - New App
 {{< figure src="/apigee/apigee-tutorial7_27.jpg" >}}

 ```
 Name: myapp
 Display name: myapp
 Developer name: hskim@hancom.com
 Callback URL: 공란
 Notes: 공란
 Expiry: Never
 Product: myproduct
 Custom attributes: 공란
 ```

- 추가 화면
 {{< figure src="/apigee/apigee-tutorial7_28.jpg" >}}

- API키를 복사한다. 
 ```
 Key: 8mE1cvb3NFcp9S5dkz1tuWxyCAVpX66nPcGpCAWDZvbNTjPm
 Secret: EYUeAtwGTky4XMOT2T0yI2tpXrZyNKFbWWyfU59ayOjP1ht591**************
 ```

 ### 8. curl 호출 확인
 ```
 curl -v https://$PUBLIC_FACING_IP/helloworld?apikey=ZQA5euYtNeJ7ZCGCJMpvd6F2BZOmxOzY
 ```

 ```
 $ curl -v https://spsenti2023.duckdns.org/helloworld?apikey=8mE1cvb3NFcp9S5dkz1tuWxyCAVpX66nPcGpCAWDZvbNTjPm
*   Trying 34.117.255.14:443...
* Connected to spsenti2023.duckdns.org (34.117.255.14) port 443 (#0)
* schannel: disabled automatic use of client certificate
* schannel: ALPN, offering http/1.1
* schannel: ALPN, server accepted to use http/1.1
> GET /helloworld?apikey=8mE1cvb3NFcp9S5dkz1tuWxyCAVpX66nPcGpCAWDZvbNTjPm HTTP/1.1
> Host: spsenti2023.duckdns.org
> User-Agent: curl/7.79.1
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< x-powered-by: Apigee
< access-control-allow-origin: *
< x-frame-options: ALLOW-FROM RESOURCE-URL
< x-xss-protection: 1
< x-content-type-options: nosniff
< content-type: application/json;charset=UTF-8
< content-length: 77
< etag: W/"8d-/7TqkgBKcDi8Ug3uWWUJpw"
< date: Thu, 03 Mar 2022 06:44:20 GMT
< alt-svc: clear
< x-request-id: ca4e02c3-7ef5-4367-9d1d-48c3f5a8f896
< Via: 1.1 google, 1.1 google
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
{"root":{"city":"San Jose","firstName":"John","lastName":"Doe","state":"CA"}}* Connection #0 to host spsenti2023.duckdns.org left intact
 ```

 > API archive가 Apigee 환경에 성공적으로 배포되었습니다. 

---

### 2. 환경 그룹 
```
curl -i -H "$AUTH" -H "Content-Type:application/json" "https://apigee.googleapis.com/v1/organizations/$PROJECT_ID/environments/dev"
```

[인증 에러]
```
$ curl -i -H "$AUTH" -H "Content-Type:application/json" "https://apigee.googleapis.com/v1/organizations/pure-fold-339305/environments/dev"
HTTP/2 401 
www-authenticate: Bearer realm="https://accounts.google.com/"
vary: X-Origin
vary: Referer
vary: Origin,Accept-Encoding
content-type: application/json; charset=UTF-8
date: Thu, 24 Feb 2022 06:00:30 GMT
server: ESF
cache-control: private
x-xss-protection: 0
x-frame-options: SAMEORIGIN
x-content-type-options: nosniff
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
accept-ranges: none

{
  "error": {
    "code": 401,
    "message": "Request is missing required authentication credential. Expected OAuth 2 access token, login cookie or other valid authentication credential. See https://developers.google.com/identity/sign-in/web/devconsole-project.",
    "status": "UNAUTHENTICATED",
    "details": [
      {
        "@type": "type.googleapis.com/google.rpc.ErrorInfo",
        "reason": "CREDENTIALS_MISSING",
        "domain": "googleapis.com",
        "metadata": {
          "service": "apigee.googleapis.com",
          "method": "google.cloud.apigee.v1.EnvironmentService.GetEnvironment"
        }
      }
    ]
  }
}
```

[오류확인](https://developers.google.com/identity/sign-in/web/sign-in)

> 액세스 토큰 확인
```
$ gcloud auth application-default print-access-token   
ya29.A0ARrdaM8TiVeqbSujEaiw59ZtMo0N-jgOxWEO5SZoRFpB4BweBlak6C35aKe9BrBgM4E5kKfIOmY2kwZFJDgukeVA52AjKUhRuGfpHafj2iH46PBEAaBZwijK5erBG94VgIO1Qgb1R**************************


curl -s -H "Content-Type: application/json" -H "Authorization: Bearer "$(gcloud auth application-default print-access-token)   https://apigee.googleapis.com/v1/organizations/pure-fold-339305/environments/dev -d @sync-request.json

```

[Google Developers](https://developers.google.com/oauthplayground/)



