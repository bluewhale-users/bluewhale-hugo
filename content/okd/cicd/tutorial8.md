---
title: "Tutorial8"
date: 2022-03-15T11:32:36+09:00
weight: 48
---

# ArgoCD 설치

## 1. ArgoCD Operator 이동
```
- okd -> Administrator -> Operators -> Installed Operators 이동
```
{{< figure src="/cicd/tutorial8_1.jpg" >}}

## 2. ArgoCD 탭으로 이동후 Create ArgoCD 선택
{{< figure src="/cicd/tutorial8_2.jpg" >}}
{{< figure src="/cicd/tutorial8_3.jpg" >}}
{{< figure src="/cicd/tutorial8_4.jpg" >}}

## 3. Developer로 변경후 Topology 확인
```
- okd -> Developer -> Topology
```
{{< figure src="/cicd/tutorial8_5.jpg" >}}

## 4. ArgoCD Admin 패스워드 확인
```
- okd -> Developer -> Secrets 이동
- cluster 검색
```
{{< figure src="/cicd/tutorial8_6.jpg" >}}

### argocd-sample-cluster 시크릿 확인
{{< figure src="/cicd/tutorial8_7.jpg" >}}

### Reveal values 클릭 (복호화된 admin password를 확인할 수 있다.)
{{< figure src="/cicd/tutorial8_8.jpg" >}}

```
r8BtkSKu3J0ex4TXUbsoDYMw************
```

> [Tip] 암호 변경은 YAML 탭으로 변경후 admin.password: 필드에 base64로 인코딩한 암호를 붙여넣는다.


## 5. Topology로 이동후 argocd-sample-server의 OpenURL을 선택한다. 
```
Username : admin
Password : r8BtkSKu3J0ex4TXUbs***********
```
{{< figure src="/cicd/tutorial8_9.jpg" >}}

{{< figure src="/cicd/tutorial8_10.jpg" >}}

