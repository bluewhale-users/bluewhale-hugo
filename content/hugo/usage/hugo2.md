---
title: "Hugo2 : 사이트 구축"
date: 2022-03-22T11:24:17+09:00
draft: true
weight: 42
---



### 1. Hugo 설치
- [Hugo Quick-Start](https://gohugo.io/getting-started/quick-start/)
  
#### 1.1 hugo 설치(windows 기준 설명)
* [Hugo Download](https://github.com/gohugoio/hugo/releases)
* hugo release에서 최신버전을 다운로드
* C:\Hugo\bin\에 압축 해제
* 환경변수에 경로 추가  
  * window + Q로 검색창을 연 뒤 환경 변수를 검색해서 환경 변수 선택  
  * 시스템변수의 Path를 더블클릭한다.  
  * 새로 만들기를 클릭한 다음 아까 압축을 풀었던 곳인 C:\Hugo\bin를 등록  
* command에서 hugo version을 쳐서 확인

{{< tabs >}}
{{% tab name="windows" %}}
```windows
C:\Users\user>hugo version
hugo v0.94.0-63B23660 windows/amd64 BuildDate=2022-03-10T09:46:36Z VendorInfo=gohugoio
```
{{% /tab %}}
{{% tab name="MacOS" %}}
```Bash
brew install hugo
# or
port install hugo
```
{{% /tab %}}
{{< /tabs >}}



#### 1.2 Hugo 프로젝트 만들기
- hugo new site <프로젝트 이름>
```
$hugo new site bluewhale-hugo
Congratulations! Your new Hugo site is created in D:\Git\bluewhale\bluewhale-hugo.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

- Directory 구조
``` base
C:\bluewhale-hugo
├─archetypes
├─content
├─data
├─layouts
├─static
└─themes
```

### 2. 테마 추가
#### 2.1 Hugo theme 다운로드
- [hugo theme](https://themes.gohugo.io/)
- [techdoc theme : MIT](https://github.com/thingsym/hugo-theme-techdoc)

{{< tabs >}}
{{% tab name="windows" %}}
```windows
$ cd bluewhale-hugo
$ git submodule add https://github.com/thingsym/hugo-theme-techdoc.git themes/hugo-theme-techdoc
$ git submodule update --remote
$ git add themes/hugo-theme-techdoc
```
{{% /tab %}}
{{< /tabs >}}

#### 2.2 미리보기
{{< tabs >}}
{{% tab name="windows" %}}
```windows
hugo server -D
# -D draft 문서도 보여준다. 
```
{{% /tab %}}
{{< /tabs >}}

```
$ hugo server -D
port 1313 already in use, attempting to use an available port
Start building sites … 
hugo v0.94.0-63B23660 windows/amd64 BuildDate=2022-03-10T09:46:36Z VendorInfo=gohugoio

                   | EN  
-------------------+-----
  Pages            | 14  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  5  
  Processed images |  0  
  Aliases          |  0  
  Sitemaps         |  1
  Cleaned          |  0

Built in 64 ms
Watching for changes in D:\Git\bluewhale\bluewhale-hugo\{archetypes,content,data,layouts,static,themes}
Watching for config changes in D:\Git\bluewhale\bluewhale-hugo\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:8868/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

#### 2.3 빌드
{{< tabs >}}
{{% tab name="windows" %}}
```windows
# hugo -t <테마이름>
hugo server -t hugo-theme-techdoc

# 출력위치 지정
# hugo -t hugo-theme-techdoc -d public_html
```
{{% /tab %}}
{{< /tabs >}}

```
$ hugo server -t hugo-theme-techdoc
Start building sites …
hugo v0.94.0-63B23660 windows/amd64 BuildDate=2022-03-10T09:46:36Z VendorInfo=gohugoio

                   | EN
-------------------+-----
  Pages            |  7
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  5
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 87 ms
Watching for changes in D:\Git\bluewhale\bluewhale-hugo\{archetypes,content,data,layouts,static,themes}
Watching for config changes in D:\Git\bluewhale\bluewhale-hugo\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

- public 폴더에 추가됨  
{{< figure src="/hugo/hugo1_5.jpg" >}}

- [http://localhost:1313](http://localhost:1313) 접속 화면
{{< figure src="/hugo/hugo1_4.jpg" >}}

#### 2.4 새 글 추가
```
$ hugo new post/test.md
Content "D:\\Git\\bluewhale\\bluewhale-hugo\\content\\post\\test.md" created
```

### 3. 리파지토리 생성

2개의 리파지토리를 생성한다. 
1) 전체 컨텐츠를 저장할 곳
2) 빌드 결과로 github page를 띄울 곳

첫번째 repository는 <프로젝트 이름>
두번째 repository는 #USER-ID.github.io로 만들면 된다.

- [bluewhale-hugo](https://github.com/bluewhale-users/bluewhale-hugo)
- [bluewhale.github.io](https://github.com/bluewhale-users/bluewhale.github.io)

#### 3.1 git remote 설정
```
$ cd bluewhale-hugo
$ git init
$ git remote add origin https://github.com/bluewhale-users/bluewhale-hugo
```

#### 3.2 github page 리파지토리 연결(bluewhale.github.io)
```
$ git submodule add -b master https://github.com/bluewhale-users/bluewhale.github.io.git public
```

```
$ git submodule add -b master https://github.com/bluewhale-users/bluewhale.github.io.git public
Cloning into 'D:/Git/bluewhale/bluewhale-hugo/public'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), done.
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory
```

#### 3.3 commit/push

```
$ git commit
$ git push
```

{{% notice warning %}}
pull 실행시 아래와 같은 에러가 나온다면 히스토리를 리셋한다.  
{{% /notice %}}

```
> git pull --tags origin master
From https://github.com/bluewhale-users/bluewhale-hugo
 * branch            master     -> FETCH_HEAD
fatal: refusing to merge unrelated histories
```

```
# git pull origin 브런치명 --allow-unrelated-histories
git pull origin master --allow-unrelated-histories
``` 


