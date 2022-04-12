---
title: "Tutorial5 : Add From Container Image"
date: 2022-04-12T15:10:00+09:00
draft: false
weight: 45
---

- [sample github](https://github.com/bluewhale-users/okd-tutorial2-src)

### 1. Sample Code Clone

{{< tabs >}}
{{% tab name="windows" %}}
```windows
> git clone git@github.com:bluewhale-users/okd-tutorial2-src.git
Cloning into 'okd-tutorial2-src'...
remote: Enumerating objects: 23, done.
remote: Counting objects: 100% (23/23), done.
remote: Compressing objects:  16% (3/18)
Resolving deltas: 100% (1/1), done.6/18)
remote: Compressing objects: 100% (18/18), done.
remote: Total 23 (delta 1), reused 19 (delta 1), pack-reused 0
```
{{% /tab %}}
{{< /tabs >}}

### 2. visual studio code로 열기
{{< tabs >}}
{{% tab name="windows" %}}
```windows
> cd okd-tutorial2-src
> code ./
```
{{% /tab %}}
{{< /tabs >}}

{{< figure src="/web-console/tutorial5_1.jpg" >}}

### 3. Dockerfile을 이용한 이미지 빌드
{{< figure src="/web-console/tutorial5_2.jpg" >}}

### 4. 이미지 이름 입력
{{< figure src="/web-console/tutorial5_3.jpg" >}}

### 5. 빌드 성공
{{< figure src="/web-console/tutorial5_4.jpg" >}}

### 6. 이미지 실행
{{< figure src="/web-console/tutorial5_5.jpg" >}}

### 7. 이미지 우클릭해 "Run" 실행
{{< figure src="/web-console/tutorial5_6.jpg" >}}

### 8. 접속 port 확인
{{< figure src="/web-console/tutorial5_7.jpg" >}}

```
> Executing task: docker run --rm -d  -p 3000:3000/tcp tutorial2-src:latest <
```

### 9. 실행 확인
{{< figure src="/web-console/tutorial5_8.jpg" >}}

### 10. 브라우저에서 접속 확인
```
http://localhost:3000
```

{{< figure src="/web-console/tutorial5_9.jpg" >}}


### 11. Dockerhub에 이미지 업로드
- [dockerhub Home](https://hub.docker.com/)
- [dockerhub 설정 참고]({{< ref "/okd/cicd/tutorial3.md" >}})

- dockerhub 접속
{{< figure src="/web-console/tutorial5_10.jpg" >}}

- Create Repository 선택
{{< figure src="/web-console/tutorial5_11.jpg" >}}

- 리파지터리 이름을 입력후 public 저장소로 만든다.
{{< figure src="/web-console/tutorial5_12.jpg" >}}

- 저장소 생성
{{< figure src="/web-console/tutorial5_13.jpg" >}}

- push command
```
docker push spcsenti/tutorial2-src:tagname
```

- docker login
```
>docker login -u "your id"
Password:
Login Succeeded

Logging in with your password grants your terminal complete access to your account.
For better security, log in with a limited-privilege personal access token. Learn more at https://docs.docker.com/go/access-tokens/
```

```

// 이미지 태그 변경
> docker tag tutorial2-src:latest "your id"/tutorial2-src:latest
> docker push "your id"/tutorial2-src:latest
```

```
>docker tag tutorial2-src:latest "your id"/tutorial2-src:latest

>docker push "your id"/tutorial2-src:latest
The push refers to repository [docker.io/"your id"/tutorial2-src]
60ecf9354b04: Pushed
68a6cff145b3: Pushed
11eaee07b9a1: Pushed
af05d497050a: Pushed
da7b93b499cd: Pushed
6cfd9fa8083f: Pushed
78bb105cd27d: Pushed
c26a5692b560: Pushed
0cd41aa80b1f: Pushed
7a6d0f54488f: Pushed
6ef8823b489f: Pushed
9578c16f3f7c: Pushed
3141322c5cdb: Pushed
latest: digest: sha256:2951d4484879a51e1eae869c394cb49e0879e8f633a918efe94a5242736a85be size: 3050
```

- 이미지 업로드 확인
{{< figure src="/web-console/tutorial5_14.jpg" >}}

### 12. Add to Project -> Container Image 선택
{{< figure src="/web-console/tutorial5_15.jpg" >}}

- 레지스트리 주소 입력(다른 설정은 기본값 사용)
{{< figure src="/web-console/tutorial5_16.jpg" >}}

```
레지스트리 주소 : docker.io/spcsenti/tutorial2-src:latest
```

- 배포 확인
{{< figure src="/web-console/tutorial5_17.jpg" >}}

- 접속 확인
{{< figure src="/web-console/tutorial5_18.jpg" >}}

