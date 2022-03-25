---
title: "Hugo1 : Hugo 소개"
date: 2022-03-22T11:23:48+09:00
draft: false
weight: 41
---

### 1. Hugo 
- [gohugo.io](https://gohugo.io/)  
- [hugo github](https://github.com/gohugoio/hugo)    
- [shortcodes](https://gohugo.io/content-management/shortcodes/)

휴고(Hugo)는 Go로 작성된 정적 사이트[^footnote1] 생성기입니다. 웹페이지 접속시 실시간으로 페이지를 생성하는 동적사이트[^footnote2]와 달리 휴고는 컨텐츠를 만들거나 업데이트시 페이지를 생성합니다. 따라서 휴고로 구축된 웹사이트는 일반적으로 더 빠르고 안전합니다.

장점
- 빌드 시간이 매우 빠르다. 
- 다양한 OS에서 쉽게 설치하여 개발할 수 있다. 
- LiveReload 기능을 제공해 변경사항을 즉시 렌더링해 확인할 수 있다. 
- 다양한 테마가 존재한다. 
- 정적 사이트를 렌더링하므로 제한없이 모든곳에서 호스팅할 수 있다. 


[^footnote1]: static site는 고정된 html을 그냥 뿌려주는 사이트이다. 따라서 static site를 쓴다면 언제 들어간다고 해도 항상 같은 화면만 나온다.

[^footnote2]: Dynamic site 그때그때 동적으로 html을 생성해서 보여주는 사이트다. 즉, dynamic site의 화면은 같은 주소라도 지속적으로 변할 수 있다. 