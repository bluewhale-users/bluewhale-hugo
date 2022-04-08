---
title: "Tutorial2 : 프로젝트 만들기"
date: 2022-04-07T12:11:44+09:00
draft: false
weight: 42
---

### 1. 프로젝트 만들기
- Administrator -> Home -> Projects 이동
{{< figure src="/web-console/tutorial2_1.jpg" >}}  

### 2. Create Project 선택
- Name, Display name, Description 입력
{{< figure src="/web-console/tutorial2_2.jpg" >}}  

### 3. 프로젝트 생성 화면
{{< figure src="/web-console/tutorial2_3.jpg" >}}  

### 4. 개발자(Developer)관점 보기로 전환
{{< figure src="/web-console/tutorial2_4.jpg" >}}  

### 5. 토폴로지 화면
- 현재 빈프로젝트이기 때문에 아무것도 보이지 않는다. 
{{< figure src="/web-console/tutorial2_5.jpg" >}}  

### 5. Application 배포해보기
- 화면에서 우클릭하여 메뉴 확인(Samples 선택)
{{< figure src="/web-console/tutorial2_6.jpg" >}}  

### 6. 코드 샘플을 사용하여 어플리케이션을 생성(Nginx)
- Nginx 선택
{{< figure src="/web-console/tutorial2_19.jpg" >}}  

### 7. Name 입력(my-nginx-sample)
- [source github](https://github.com/sclorg/nginx-ex)
{{< figure src="/web-console/tutorial2_20.jpg" >}}  

### 8. 빌드중 상태가 종료될때까지 대기한다. 
{{< figure src="/web-console/tutorial2_21.jpg" >}}  

### 9. 빌드 성공
{{< figure src="/web-console/tutorial2_22.jpg" >}}  

### 10. OpenURL을 통해 서비스에 접속
{{< figure src="/web-console/tutorial2_23.jpg" >}}

- 접속 화면
{{< figure src="/web-console/tutorial2_24.jpg" >}}

---
### 11. 코드 샘플을 사용하여 어플리케이션을 생성(node.js)
- Node.js 선택
- [source github](https://github.com/sclorg/nodejs-ex )
{{< figure src="/web-console/tutorial2_7.jpg" >}}  

### 12. 샘플 어플리케이션 생성 화면
- 이름변경(나머지는 기본값 사용)후 create를 클릭한다. 
{{< figure src="/web-console/tutorial2_8.jpg" >}}  

### 13. 빌드중 상태가 종료될때까지 대기한다. 
{{< figure src="/web-console/tutorial2_9.jpg" >}}  

### 14. 빌드 성공
{{< figure src="/web-console/tutorial2_10.jpg" >}}

### 15. OpenURL을 통해 서비스에 접속
{{< figure src="/web-console/tutorial2_11.jpg" >}}

- 접속 화면  
{{< figure src="/web-console/tutorial2_12.jpg" >}}

### 16. DB 연결
- 방문 횟수가 카운트되어 보여야 하지만 DB 연결 실패 메시지가 출력된다. 
{{< figure src="/web-console/tutorial2_13.jpg" >}}

- oc cli를 사용해 MongoDB 배포

{{< tabs >}}
{{% tab name="windows" %}}
```windows
#project를 위에서 생성한 프로젝트로 변경한다. 
$ oc project okd-tutorials
Now using project "okd-tutorials" on server "https://api.your-okd.com:6443".
```
{{% /tab %}}
{{< /tabs >}}

- mongo-db 배포


{{< tabs >}}
{{% tab name="windows" %}}
```windows
$ oc new-app centos/mongodb-26-centos7 \
  -e MONGODB_USER=admin \
  -e MONGODB_DATABASE=mongo_db \
  -e MONGODB_PASSWORD=secret \
  -e MONGODB_ADMIN_PASSWORD=super-secret 
```
{{% /tab %}}
{{< /tabs >}}

```
C:\Users\user>oc new-app centos/mongodb-26-centos7 -e MONGODB_USER=admin -e MONGODB_DATABASE=mongo_db -e MONGODB_PASSWORD=secret -e MONGODB_ADMIN_PASSWORD=super-secret
--> Found container image ed70d49 (3 years old) from Docker Hub for "centos/mongodb-26-centos7"

    MongoDB 2.6
    -----------
    MongoDB (from humongous) is a free and open-source cross-platform document-oriented database program. Classified as a NoSQL database program, MongoDB uses JSON-like documents with schemas. This container image contains programs to run mongod server.

    Tags: database, mongodb, rh-mongodb26

    * An image stream tag will be created as "mongodb-26-centos7:latest" that will track this image

--> Creating resources ...
    deployment.apps "mongodb-26-centos7" created
    service "mongodb-26-centos7" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/mongodb-26-centos7'
    Run 'oc status' to view your app.
```

- oc status로 상태 확인
```
$ oc status
In project okd turotials (okd-tutorials) on server https://api.your-okd.com:6443

svc/mongodb-26-centos7 - 172.30.127.231:27017
  deployment/mongodb-26-centos7 deploys istag/mongodb-26-centos7:latest
    deployment #2 running for 2 minutes - 0/1 pods growing to 1
    deployment #1 deployed 2 minutes ago - 0/1 pods growing to 1

http://my-nodejs-sample-okd-tutorials.apps.api.your-okd.com to pod port 8080-tcp (svc/my-nodejs-sample)
  deployment/my-nodejs-sample deploys istag/my-nodejs-sample:latest <-
    bc/my-nodejs-sample source builds https://github.com/sclorg/nodejs-ex.git on openshift/nodejs:14-ubi7
    deployment #2 running for 24 minutes - 0/1 pods growing to 1
    deployment #1 deployed 35 minutes ago - 1 pod


2 infos identified, use 'oc status --suggest' to see details.
```

{{% notice info %}}
MongoDB 인스턴스 URL : 172.30.127.231:27017  
Nodejs Deployment : deployment/my-nodejs-sample
{{% /notice %}}

- MongoDB 인스턴스 URL 확인(172.30.127.231:27017)

- Pod 환경 변수 확인
```
oc set env pods --all --list
```

```
$ oc set env pods --all --list
# pods/my-nodejs-sample-1-build, container sti-build
BUILD={"kind":"Build","apiVersion":"build.openshift.io/v1","metadata":{"name":"my-nodejs-sample-1","namespace":"okd-tutorials","uid":"c8217c38-6604-49ac-94f1-fff0afd6728e","resourceVersion":"317857363","generation":1,"creationTimestamp":"2022-04-07T03:26:42Z","labels":{"app":"my-nodejs-sample","app.kubernetes.io/component":"my-nodejs-sample","app.kubernetes.io/instance":"my-nodejs-sample","app.kubernetes.io/name":"my-nodejs-sample","app.kubernetes.io/part-of":"sample-app","app.openshift.io/runtime":"nodejs","app.openshift.io/runtime-version":"14-ubi7","buildconfig":"my-nodejs-sample","openshift.io/build-config.name":"my-nodejs-sample","openshift.io/build.start-policy":"Serial"},"annotations":{"openshift.io/build-config.name":"my-nodejs-sample","openshift.io/build.number":"1"},"ownerReferences":[{"apiVersion":"build.openshift.io/v1","kind":"BuildConfig","name":"my-nodejs-sample","uid":"e8bdacd0-e875-498c-b9ec-0e83ae10b9f0","controller":true}],"managedFields":[{"manager":"openshift-apiserver","operation":"Update","apiVersion":"build.openshift.io/v1","time":"2022-04-07T03:26:42Z","fieldsType":"FieldsV1","fieldsV1":{"f:metadata":{"f:annotations":{".":{},"f:openshift.io/build-config.name":{},"f:openshift.io/build.number":{}},"f:labels":{".":{},"f:app":{},"f:app.kubernetes.io/component":{},"f:app.kubernetes.io/instance":{},"f:app.kubernetes.io/name":{},"f:app.kubernetes.io/part-of":{},"f:app.openshift.io/runtime":{},"f:app.openshift.io/runtime-version":{},"f:buildconfig":{},"f:openshift.io/build-config.name":{},"f:openshift.io/build.start-policy":{}},"f:ownerReferences":{".":{},"k:{\"uid\":\"e8bdacd0-e875-498c-b9ec-0e83ae10b9f0\"}":{".":{},"f:apiVersion":{},"f:controller":{},"f:kind":{},"f:name":{},"f:uid":{}}}},"f:spec":{"f:output":{"f:to":{".":{},"f:kind":{},"f:name":{}}},"f:serviceAccount":{},"f:source":{"f:git":{".":{},"f:uri":{}},"f:type":{}},"f:strategy":{"f:sourceStrategy":{".":{},"f:from":{".":{},"f:kind":{},"f:name":{}},"f:pullSecret":{".":{},"f:name":{}}},"f:type":{}},"f:triggeredBy":{}},"f:status":{"f:conditions":{".":{},"k:{\"type\":\"New\"}":{".":{},"f:lastTransitionTime":{},"f:lastUpdateTime":{},"f:status":{},"f:type":{}}},"f:config":{".":{},"f:kind":{},"f:name":{},"f:namespace":{}},"f:phase":{}}}}]},"spec":{"serviceAccount":"builder","source":{"type":"Git","git":{"uri":"https://github.com/sclorg/nodejs-ex.git"}},"strategy":{"type":"Source","sourceStrategy":{"from":{"kind":"DockerImage","name":"image-registry.openshift-image-registry.svc:5000/openshift/nodejs@sha256:a49baf4d9de05b879d319356aa9349f4ad9962fd5859f2e7029e2da1559a8d2d"},"pullSecret":{"name":"builder-dockercfg-2h2dq"}}},"output":{"to":{"kind":"DockerImage","name":"image-registry.openshift-image-registry.svc:5000/okd-tutorials/my-nodejs-sample:latest"},"pushSecret":{"name":"builder-dockercfg-2h2dq"}},"resources":{},"postCommit":{},"nodeSelector":null,"triggeredBy":[{"message":"Build configuration change"}]},"status":{"phase":"New","outputDockerImageReference":"image-registry.openshift-image-registry.svc:5000/okd-tutorials/my-nodejs-sample:latest","config":{"kind":"BuildConfig","namespace":"okd-tutorials","name":"my-nodejs-sample"},"output":{},"conditions":[{"type":"New","status":"True","lastUpdateTime":"2022-04-07T03:26:42Z","lastTransitionTime":"2022-04-07T03:26:42Z"}]}}

LANG=C.utf8
SOURCE_REPOSITORY=https://github.com/sclorg/nodejs-ex.git
SOURCE_URI=https://github.com/sclorg/nodejs-ex.git
ALLOWED_UIDS=1-
DROP_CAPS=KILL,MKNOD,SETGID,SETUID
PUSH_DOCKERCFG_PATH=/var/run/secrets/openshift.io/push
PULL_DOCKERCFG_PATH=/var/run/secrets/openshift.io/pull
BUILD_REGISTRIES_CONF_PATH=/var/run/configs/openshift.io/build-system/registries.conf
BUILD_REGISTRIES_DIR_PATH=/var/run/configs/openshift.io/build-system/registries.d
BUILD_SIGNATURE_POLICY_PATH=/var/run/configs/openshift.io/build-system/policy.json
BUILD_STORAGE_CONF_PATH=/var/run/configs/openshift.io/build-system/storage.conf
BUILD_STORAGE_DRIVER=overlay
BUILD_BLOBCACHE_DIR=/var/cache/blobs
HTTP_PROXY=
HTTPS_PROXY=
NO_PROXY=
# pods/my-nodejs-sample-564c48b655-sr592, container my-nodejs-sample
```

- Node.js 웹앱에 환경 변수를 추가
```
oc set env deployment/my-nodejs-sample MONGO_URL='mongodb://admin:secret@172.30.127.231:27017/mongo_db'
```

```
$ oc set env deployment/my-nodejs-sample MONGO_URL='mongodb://admin:secret@172.30.127.231:27017/mongo_db'
deployment.apps/my-nodejs-sample updated
```

- 업데이트 배포 확인

```
$ oc status
In project okd turotials (okd-tutorials) on server https://your-okd.com:6443

svc/mongodb-26-centos7 - 172.30.127.231:27017
  deployment/mongodb-26-centos7 deploys istag/mongodb-26-centos7:latest
    deployment #2 running for 24 minutes - 0/1 pods growing to 1
    deployment #1 deployed 24 minutes ago - 0/1 pods growing to 1

http://my-nodejs-sample-okd-tutorials.apps.blackwhale.cloud.hancom.com to pod port 8080-tcp (svc/my-nodejs-sample)
  deployment/my-nodejs-sample deploys istag/my-nodejs-sample:latest <-
    bc/my-nodejs-sample source builds https://github.com/sclorg/nodejs-ex.git on openshift/nodejs:14-ubi7
    deployment #3 running for 2 minutes - 0/1 pods growing to 1
    deployment #2 deployed 46 minutes ago
    deployment #1 deployed 57 minutes ago - 1 pod


2 infos identified, use 'oc status --suggest' to see details.
```


- 환경설정 확인
```
$ oc set env pods --all --list
...........
LANG=C.utf8
SOURCE_REPOSITORY=https://github.com/sclorg/nodejs-ex.git
SOURCE_URI=https://github.com/sclorg/nodejs-ex.git
ALLOWED_UIDS=1-
DROP_CAPS=KILL,MKNOD,SETGID,SETUID
PUSH_DOCKERCFG_PATH=/var/run/secrets/openshift.io/push
PULL_DOCKERCFG_PATH=/var/run/secrets/openshift.io/pull
BUILD_REGISTRIES_CONF_PATH=/var/run/configs/openshift.io/build-system/registries.conf
BUILD_REGISTRIES_DIR_PATH=/var/run/configs/openshift.io/build-system/registries.d
BUILD_SIGNATURE_POLICY_PATH=/var/run/configs/openshift.io/build-system/policy.json
BUILD_STORAGE_CONF_PATH=/var/run/configs/openshift.io/build-system/storage.conf
BUILD_STORAGE_DRIVER=overlay
BUILD_BLOBCACHE_DIR=/var/cache/blobs
HTTP_PROXY=
HTTPS_PROXY=
NO_PROXY=
# pods/my-nodejs-sample-7598dc4c8d-htfk6, container my-nodejs-sample
MONGO_URL='mongodb://admin:secret@172.30.127.231:27017/mongo_db'
```

### 17. mongodb 배포 화면
{{< figure src="/web-console/tutorial2_18.jpg" >}}