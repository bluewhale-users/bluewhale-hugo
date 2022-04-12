---
title: "Tutorial4 : Add From Git"
date: 2022-04-11T09:50:05+09:00
draft: false
weight: 44
---

[Sample Github](https://github.com/bluewhale-users/okd-tutorial2-src)

### 1. 프로젝트에 추가 
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


- 아래로 스크롤해 Application name과 Name을 입력한다. 
```
Builder Image version : 14-ubi7
Application name : okd-tutorial-2-src-app
Name : okd-tutorial-2-src
Resources : Deployment
Create a route to the Applicaiton : Checked
```

- Advanced options의 "Show advanced Routing options"을 확장해 Target port를 "3000"으로 변경한다. 
{{< figure src="/web-console/tutorial4_10.jpg" >}}

- Create 버튼을 누른다. (다른 옵션은 기본값 사용)

- Build가 끝날때까지 기다린다.
{{< figure src="/web-console/tutorial4_11.jpg" >}}

- Build 성공(Open URL을 눌러 접속 확인)
{{< figure src="/web-console/tutorial4_12.jpg" >}}

- 접속 화면
{{< figure src="/web-console/tutorial4_13.jpg" >}}


### 2. 생성 리소스 확인
- Administrator 관점으로 변경한다. 
{{< figure src="/web-console/tutorial4_14.jpg" >}}

- Workloads 이동
{{< figure src="/web-console/tutorial4_15.jpg" >}}

{{% notice info %}}
Pods에 보면 2개의 Pod가 보인다.  
okd-tutorial-2-src-1-build : buildconfig에 의해 생성된 build pod  
okd-tutorial-2-src-849568bdbd-hcm5r : application 동작 pod  
Status를 보면 Completed / Running상태로 build pod의 경우 종료된것을 확인할 수 있다.   
{{% /notice %}}

- Deployments
{{< figure src="/web-console/tutorial4_16.jpg" >}}

- Deployment yaml
```
kind: Deployment
apiVersion: apps/v1
metadata:
  annotations:
    alpha.image.policy.openshift.io/resolve-names: '*'
    app.openshift.io/vcs-ref: ''
    app.openshift.io/vcs-uri: 'https://github.com/bluewhale-users/okd-tutorial2-src'
    deployment.kubernetes.io/revision: '2'
    image.openshift.io/triggers: >-
      [{"from":{"kind":"ImageStreamTag","name":"okd-tutorial-2-src:latest","namespace":"okd-tutorials"},"fieldPath":"spec.template.spec.containers[?(@.name==\"okd-tutorial-2-src\")].image","pause":"false"}]
    openshift.io/generated-by: OpenShiftWebConsole
  resourceVersion: '325511288'
  name: okd-tutorial-2-src
  uid: 45cf7dcf-a426-4f55-ae1e-fe4db8b1b993
  creationTimestamp: '2022-04-11T06:42:35Z'
  generation: 2
  managedFields:
    - manager: Mozilla
      operation: Update
      apiVersion: apps/v1
      time: '2022-04-11T06:42:35Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            .: {}
            'f:alpha.image.policy.openshift.io/resolve-names': {}
            'f:app.openshift.io/vcs-ref': {}
            'f:app.openshift.io/vcs-uri': {}
            'f:image.openshift.io/triggers': {}
            'f:openshift.io/generated-by': {}
          'f:labels':
            .: {}
            'f:app': {}
            'f:app.kubernetes.io/component': {}
            'f:app.kubernetes.io/instance': {}
            'f:app.kubernetes.io/name': {}
            'f:app.kubernetes.io/part-of': {}
            'f:app.openshift.io/runtime': {}
            'f:app.openshift.io/runtime-version': {}
        'f:spec':
          'f:progressDeadlineSeconds': {}
          'f:replicas': {}
          'f:revisionHistoryLimit': {}
          'f:selector': {}
          'f:strategy':
            'f:rollingUpdate':
              .: {}
              'f:maxSurge': {}
              'f:maxUnavailable': {}
            'f:type': {}
          'f:template':
            'f:metadata':
              'f:labels':
                .: {}
                'f:app': {}
                'f:deploymentconfig': {}
            'f:spec':
              'f:containers':
                'k:{"name":"okd-tutorial-2-src"}':
                  .: {}
                  'f:imagePullPolicy': {}
                  'f:name': {}
                  'f:ports':
                    .: {}
                    'k:{"containerPort":8080,"protocol":"TCP"}':
                      .: {}
                      'f:containerPort': {}
                      'f:protocol': {}
                  'f:resources': {}
                  'f:terminationMessagePath': {}
                  'f:terminationMessagePolicy': {}
              'f:dnsPolicy': {}
              'f:restartPolicy': {}
              'f:schedulerName': {}
              'f:securityContext': {}
              'f:terminationGracePeriodSeconds': {}
    - manager: openshift-controller-manager
      operation: Update
      apiVersion: apps/v1
      time: '2022-04-11T06:52:11Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:spec':
          'f:template':
            'f:spec':
              'f:containers':
                'k:{"name":"okd-tutorial-2-src"}':
                  'f:image': {}
    - manager: kube-controller-manager
      operation: Update
      apiVersion: apps/v1
      time: '2022-04-11T13:03:09Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            'f:deployment.kubernetes.io/revision': {}
        'f:status':
          'f:availableReplicas': {}
          'f:conditions':
            .: {}
            'k:{"type":"Available"}':
              .: {}
              'f:lastTransitionTime': {}
              'f:lastUpdateTime': {}
              'f:message': {}
              'f:reason': {}
              'f:status': {}
              'f:type': {}
            'k:{"type":"Progressing"}':
              .: {}
              'f:lastTransitionTime': {}
              'f:lastUpdateTime': {}
              'f:message': {}
              'f:reason': {}
              'f:status': {}
              'f:type': {}
          'f:observedGeneration': {}
          'f:readyReplicas': {}
          'f:replicas': {}
          'f:updatedReplicas': {}
  namespace: okd-tutorials
  labels:
    app: okd-tutorial-2-src
    app.kubernetes.io/component: okd-tutorial-2-src
    app.kubernetes.io/instance: okd-tutorial-2-src
    app.kubernetes.io/name: okd-tutorial-2-src
    app.kubernetes.io/part-of: okd-tutorial-2-src-app
    app.openshift.io/runtime: nodejs
    app.openshift.io/runtime-version: 14-ubi7
spec:
  replicas: 1
  selector:
    matchLabels:
      app: okd-tutorial-2-src
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: okd-tutorial-2-src
        deploymentconfig: okd-tutorial-2-src
    spec:
      containers:
        - name: okd-tutorial-2-src
          image: >-
            image-registry.openshift-image-registry.svc:5000/okd-tutorials/okd-tutorial-2-src@sha256:48c85bcc4823432914e234aaac9b1d01c2265e430d46dae933079a66de26609f
          ports:
            - containerPort: 8080
              protocol: TCP
          resources: {}
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
          imagePullPolicy: Always
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
      dnsPolicy: ClusterFirst
      securityContext: {}
      schedulerName: default-scheduler
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 25%
      maxSurge: 25%
  revisionHistoryLimit: 10
  progressDeadlineSeconds: 600
status:
  observedGeneration: 2
  replicas: 1
  updatedReplicas: 1
  readyReplicas: 1
  availableReplicas: 1
  conditions:
    - type: Progressing
      status: 'True'
      lastUpdateTime: '2022-04-11T06:52:17Z'
      lastTransitionTime: '2022-04-11T06:42:35Z'
      reason: NewReplicaSetAvailable
      message: ReplicaSet "okd-tutorial-2-src-849568bdbd" has successfully progressed.
    - type: Available
      status: 'True'
      lastUpdateTime: '2022-04-11T13:03:09Z'
      lastTransitionTime: '2022-04-11T13:03:09Z'
      reason: MinimumReplicasAvailable
      message: Deployment has minimum availability.

```

{{% notice info %}}
Deployment 명세서이다. 
{{% /notice %}}

- Networking -> Services
{{< figure src="/web-console/tutorial4_17.jpg" >}}

- Service yaml
```
kind: Service
apiVersion: v1
metadata:
  name: okd-tutorial-2-src
  namespace: okd-tutorials
  uid: 975ce49c-7baf-479b-a0a7-4f1ea181fe77
  resourceVersion: '324921394'
  creationTimestamp: '2022-04-11T06:42:35Z'
  labels:
    app: okd-tutorial-2-src
    app.kubernetes.io/component: okd-tutorial-2-src
    app.kubernetes.io/instance: okd-tutorial-2-src
    app.kubernetes.io/name: okd-tutorial-2-src
    app.kubernetes.io/part-of: okd-tutorial-2-src-app
    app.openshift.io/runtime: nodejs
    app.openshift.io/runtime-version: 14-ubi7
  annotations:
    app.openshift.io/vcs-ref: ''
    app.openshift.io/vcs-uri: 'https://github.com/bluewhale-users/okd-tutorial2-src'
    openshift.io/generated-by: OpenShiftWebConsole
  managedFields:
    - manager: Mozilla
      operation: Update
      apiVersion: v1
      time: '2022-04-11T06:42:35Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            .: {}
            'f:app.openshift.io/vcs-ref': {}
            'f:app.openshift.io/vcs-uri': {}
            'f:openshift.io/generated-by': {}
          'f:labels':
            .: {}
            'f:app': {}
            'f:app.kubernetes.io/component': {}
            'f:app.kubernetes.io/instance': {}
            'f:app.kubernetes.io/name': {}
            'f:app.kubernetes.io/part-of': {}
            'f:app.openshift.io/runtime': {}
            'f:app.openshift.io/runtime-version': {}
        'f:spec':
          'f:ports':
            .: {}
            'k:{"port":3000,"protocol":"TCP"}':
              .: {}
              'f:name': {}
              'f:port': {}
              'f:protocol': {}
              'f:targetPort': {}
            'k:{"port":8080,"protocol":"TCP"}':
              .: {}
              'f:name': {}
              'f:port': {}
              'f:protocol': {}
              'f:targetPort': {}
          'f:selector':
            .: {}
            'f:app': {}
            'f:deploymentconfig': {}
          'f:sessionAffinity': {}
          'f:type': {}
spec:
  ports:
    - name: 8080-tcp
      protocol: TCP
      port: 8080
      targetPort: 8080
    - name: 3000-tcp
      protocol: TCP
      port: 3000
      targetPort: 3000
  selector:
    app: okd-tutorial-2-src
    deploymentconfig: okd-tutorial-2-src
  clusterIP: 172.30.80.194
  clusterIPs:
    - 172.30.80.194
  type: ClusterIP
  sessionAffinity: None
  ipFamilies:
    - IPv4
  ipFamilyPolicy: SingleStack
status:
  loadBalancer: {}

```

{{% notice info %}}
Service 명세서이다. 
spec 필드를 확인하면 8080-tcp와 추가한 3000-tcp를 확인할 수 있다. 
{{% /notice %}}

- Networking -> Routes
{{< figure src="/web-console/tutorial4_18.jpg" >}}

- Route  yaml
```
kind: Route
apiVersion: route.openshift.io/v1
metadata:
  name: okd-tutorial-2-src
  namespace: okd-tutorials
  uid: b5934f14-6234-4770-9208-93c7ca556ce9
  resourceVersion: '324921407'
  creationTimestamp: '2022-04-11T06:42:36Z'
  labels:
    app: okd-tutorial-2-src
    app.kubernetes.io/component: okd-tutorial-2-src
    app.kubernetes.io/instance: okd-tutorial-2-src
    app.kubernetes.io/name: okd-tutorial-2-src
    app.kubernetes.io/part-of: okd-tutorial-2-src-app
    app.openshift.io/runtime: nodejs
    app.openshift.io/runtime-version: 14-ubi7
  annotations:
    openshift.io/host.generated: 'true'
  managedFields:
    - manager: Mozilla
      operation: Update
      apiVersion: route.openshift.io/v1
      time: '2022-04-11T06:42:36Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:labels':
            .: {}
            'f:app': {}
            'f:app.kubernetes.io/component': {}
            'f:app.kubernetes.io/instance': {}
            'f:app.kubernetes.io/name': {}
            'f:app.kubernetes.io/part-of': {}
            'f:app.openshift.io/runtime': {}
            'f:app.openshift.io/runtime-version': {}
        'f:spec':
          'f:port':
            .: {}
            'f:targetPort': {}
          'f:to':
            'f:kind': {}
            'f:name': {}
            'f:weight': {}
          'f:wildcardPolicy': {}
    - manager: openshift-router
      operation: Update
      apiVersion: route.openshift.io/v1
      time: '2022-04-11T06:42:36Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:status':
          'f:ingress': {}
spec:
  host: okd-tutorial-2-src-okd-tutorials.apps.blackwhale.cloud.hancom.com
  to:
    kind: Service
    name: okd-tutorial-2-src
    weight: 100
  port:
    targetPort: 3000-tcp
  wildcardPolicy: None
status:
  ingress:
    - host: okd-tutorial-2-src-okd-tutorials.apps.blackwhale.cloud.hancom.com
      routerName: default
      conditions:
        - type: Admitted
          status: 'True'
          lastTransitionTime: '2022-04-11T06:42:36Z'
      wildcardPolicy: None
      routerCanonicalHostname: router-default.apps.blackwhale.cloud.hancom.com

```

{{% notice info %}}
route 명세서이다. 
spec 필드를 확인하면 targetPort가 3000-tcp로 맵핑된것을 확인할 수 있다. 
{{% /notice %}}

- Builds -> BuildConfigs
{{< figure src="/web-console/tutorial4_19.jpg" >}}

- Build yaml
```
kind: Build
apiVersion: build.openshift.io/v1
metadata:
  annotations:
    openshift.io/build-config.name: okd-tutorial-2-src
    openshift.io/build.number: '1'
    openshift.io/build.pod-name: okd-tutorial-2-src-1-build
  resourceVersion: '324932856'
  name: okd-tutorial-2-src-1
  uid: fadbbbcb-ff4e-48e4-8f1e-8c9b92da06e3
  creationTimestamp: '2022-04-11T06:42:35Z'
  generation: 2
  namespace: okd-tutorials
  ownerReferences:
    - apiVersion: build.openshift.io/v1
      kind: BuildConfig
      name: okd-tutorial-2-src
      uid: 9c674a5b-1542-45f3-bf46-07706afec6cf
      controller: true
  labels:
    app: okd-tutorial-2-src
    app.kubernetes.io/part-of: okd-tutorial-2-src-app
    app.kubernetes.io/instance: okd-tutorial-2-src
    openshift.io/build-config.name: okd-tutorial-2-src
    app.kubernetes.io/component: okd-tutorial-2-src
    openshift.io/build.start-policy: Serial
    buildconfig: okd-tutorial-2-src
    app.openshift.io/runtime: nodejs
    app.kubernetes.io/name: okd-tutorial-2-src
    app.openshift.io/runtime-version: 14-ubi7
spec:
  nodeSelector: null
  output:
    to:
      kind: ImageStreamTag
      name: 'okd-tutorial-2-src:latest'
    pushSecret:
      name: builder-dockercfg-2h2dq
  resources: {}
  triggeredBy:
    - message: Build configuration change
  strategy:
    type: Source
    sourceStrategy:
      from:
        kind: DockerImage
        name: >-
          image-registry.openshift-image-registry.svc:5000/openshift/nodejs@sha256:a49baf4d9de05b879d319356aa9349f4ad9962fd5859f2e7029e2da1559a8d2d
      pullSecret:
        name: builder-dockercfg-2h2dq
  postCommit: {}
  serviceAccount: builder
  source:
    type: Git
    git:
      uri: 'https://github.com/bluewhale-users/okd-tutorial2-src'
    contextDir: /
  revision:
    type: Git
    git:
      commit: 22b290ce3dbbffd67275a9a9e20f1eb1b1cf1c80
      author:
        name: testuser
        email: testuser@gmail.com
      committer:
        name: testuser
        email: testuser@gmail.com
      message: commit
status:
  output:
    to:
      imageDigest: 'sha256:48c85bcc4823432914e234aaac9b1d01c2265e430d46dae933079a66de26609f'
  config:
    kind: BuildConfig
    namespace: okd-tutorials
    name: okd-tutorial-2-src
  outputDockerImageReference: >-
    image-registry.openshift-image-registry.svc:5000/okd-tutorials/okd-tutorial-2-src:latest
  duration: 576000000000
  startTimestamp: '2022-04-11T06:42:36Z'
  stages:
    - name: FetchInputs
      startTime: '2022-04-11T06:42:43Z'
      durationMilliseconds: 1929
      steps:
        - name: FetchGitSource
          startTime: '2022-04-11T06:42:43Z'
          durationMilliseconds: 1929
    - name: PullImages
      startTime: '2022-04-11T06:42:52Z'
      durationMilliseconds: 335713
      steps:
        - name: PullBaseImage
          startTime: '2022-04-11T06:42:52Z'
          durationMilliseconds: 335713
    - name: Build
      startTime: '2022-04-11T06:48:28Z'
      durationMilliseconds: 217903
      steps:
        - name: DockerBuild
          startTime: '2022-04-11T06:48:28Z'
          durationMilliseconds: 217903
    - name: PushImage
      startTime: '2022-04-11T06:52:06Z'
      durationMilliseconds: 5070
      steps:
        - name: PushImage
          startTime: '2022-04-11T06:52:06Z'
          durationMilliseconds: 5070
  conditions:
    - type: New
      status: 'False'
      lastUpdateTime: '2022-04-11T06:42:36Z'
      lastTransitionTime: '2022-04-11T06:42:36Z'
    - type: Pending
      status: 'False'
      lastUpdateTime: '2022-04-11T06:42:41Z'
      lastTransitionTime: '2022-04-11T06:42:41Z'
    - type: Running
      status: 'False'
      lastUpdateTime: '2022-04-11T06:52:12Z'
      lastTransitionTime: '2022-04-11T06:52:12Z'
    - type: Complete
      status: 'True'
      lastUpdateTime: '2022-04-11T06:52:12Z'
      lastTransitionTime: '2022-04-11T06:52:12Z'
  completionTimestamp: '2022-04-11T06:52:12Z'
  phase: Complete

```

{{% notice info %}}
Build 명세서이다. 
s2i 빌드를 위해 사용한다. 
{{% /notice %}}

- Builds -> ImageStreams
{{< figure src="/web-console/tutorial4_20.jpg" >}}

- ImageSteram yaml
```
kind: ImageStream
apiVersion: image.openshift.io/v1
metadata:
  annotations:
    app.openshift.io/vcs-ref: ''
    app.openshift.io/vcs-uri: 'https://github.com/bluewhale-users/okd-tutorial2-src'
    openshift.io/generated-by: OpenShiftWebConsole
  resourceVersion: '324932812'
  name: okd-tutorial-2-src
  uid: c4459beb-4714-4086-ba5f-a787af58f12e
  creationTimestamp: '2022-04-11T06:42:35Z'
  generation: 1
  managedFields:
    - manager: Mozilla
      operation: Update
      apiVersion: image.openshift.io/v1
      time: '2022-04-11T06:42:35Z'
      fieldsType: FieldsV1
      fieldsV1:
        'f:metadata':
          'f:annotations':
            .: {}
            'f:app.openshift.io/vcs-ref': {}
            'f:app.openshift.io/vcs-uri': {}
            'f:openshift.io/generated-by': {}
          'f:labels':
            .: {}
            'f:app': {}
            'f:app.kubernetes.io/component': {}
            'f:app.kubernetes.io/instance': {}
            'f:app.kubernetes.io/name': {}
            'f:app.kubernetes.io/part-of': {}
            'f:app.openshift.io/runtime': {}
            'f:app.openshift.io/runtime-version': {}
  namespace: okd-tutorials
  labels:
    app: okd-tutorial-2-src
    app.kubernetes.io/component: okd-tutorial-2-src
    app.kubernetes.io/instance: okd-tutorial-2-src
    app.kubernetes.io/name: okd-tutorial-2-src
    app.kubernetes.io/part-of: okd-tutorial-2-src-app
    app.openshift.io/runtime: nodejs
    app.openshift.io/runtime-version: 14-ubi7
spec:
  lookupPolicy:
    local: false
status:
  dockerImageRepository: >-
    image-registry.openshift-image-registry.svc:5000/okd-tutorials/okd-tutorial-2-src
  tags:
    - tag: latest
      items:
        - created: '2022-04-11T06:52:11Z'
          dockerImageReference: >-
            image-registry.openshift-image-registry.svc:5000/okd-tutorials/okd-tutorial-2-src@sha256:48c85bcc4823432914e234aaac9b1d01c2265e430d46dae933079a66de26609f
          image: >-
            sha256:48c85bcc4823432914e234aaac9b1d01c2265e430d46dae933079a66de26609f
          generation: 1

```

{{% notice info %}}
ImageStream 명세서이다. 
빌드 결과로 생성된 이미지와 관련된 정보를 알 수 있다. 
{{% /notice %}}