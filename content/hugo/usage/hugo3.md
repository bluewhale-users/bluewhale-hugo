---
title: "Hugo3 : 테마 수정 및 변경"
date: 2022-03-22T11:24:20+09:00
draft: false
weight: 43
---

### 1. Theme Overriding
테마 수정시 'themes' 디렉토리의 내용은 수정하지 않는다. 테마구조를 살펴보면 원본 프로젝트 구조와 유사한 것을 확인할 수 있다. (archetypes, layouts, static, ...), 즉 테마도 hugo 프로젝트이다.  
테마 프로젝트의 layouts 파일들을 원본 프로젝트 layouts 폴더에 복사하여 이를 수정함으로써 테마를 오버라이딩하여 사용할 수 있다. 

- \layouts\partials\header.html이 존재하면 \layouts\partials\header.html을 적용한다.
- 존재하지 않으면 \themes\<테마 이름>\layouts\partials\header.html을 적용한다

### 2. 아래 링크를 참고하여 테마를 수정해 보자. 
- [hugo-theme-techdoc exampleSite](https://github.com/thingsym/hugo-theme-techdoc/tree/master/exampleSite)

{{< tabs >}}
{{% tab name="config.toml" %}}
``` Bash
baseURL = 'https://bluewhale-users.github.io/'
languageCode = 'en-us'
title = 'Bluewhale Tutorial Site'
theme = "hugo-theme-techdoc"

hasCJKLanguage = true
metaDataFormat = "yaml"

defaultContentLanguage = "en"
defaultContentLanguageInSubdir= false
enableMissingTranslationPlaceholders = false

[params]

    # Source Code repository section
    description = "put your description"
    github_repository = "https://github.com/thingsym/hugo-theme-techdoc"
    version = "0.9.7"

    # Documentation repository section
    # documentation repository (set edit link to documentation repository)
    github_doc_repository = "https://github.com/thingsym/hugo-theme-techdoc"
    github_doc_repository_path = ""

    # Analytic section
    google_analytics_id = "" # Your Google Analytics tracking id
    tag_manager_container_id = "" # Your Google Tag Manager container id
    google_site_verification = "" # Your Google Site Verification for Search Console

    # Open Graph and Twitter Cards settings section
    # Open Graph settings for each page are set on the front matter.
    # See https://gohugo.io/templates/internal/#open-graph
    # See https://gohugo.io/templates/internal/#twitter-cards
    title = "Hugo Techdoc Theme"
    images = ["images/og-image.png"] # Open graph images are placed in `static/images`

    # Theme settings section
    # Theme color
    # See color value reference https://developer.mozilla.org/en-US/docs/Web/CSS/color
    custom_font_color = ""
    custom_background_color = ""

    # Documentation Menu section
    # Menu style settings
    menu_style = "slide-menu" # "open-menu" or "slide-menu" or "" blank is as no sidebar

    # Date format
    dateformat = "" # default "2 Jan 2006"
    # See the format reference https://gohugo.io/functions/format/#hugo-date-and-time-templating-reference

    # path name excluded from documentation menu
    menu_exclusion = [
        "archives",
        "archive",
        "blog",
        "entry",
        "post",
        "posts",
    ]

    # Algolia site search section
    # See https://www.algolia.com/doc/
    algolia_search_enable = true
    algolia_indexName = "hugo-demo-techdoc"
    algolia_appId = "7W4SAN4PLK"
    algolia_apiKey = "cbf12a63ff72d9c5dc0c10c195cf9128" # Search-Only API Key

# Global menu section
# See https://gohugo.io/content-management/menus/
[menu]
    [[menu.main]]
        name = "Home"
        url = "/"
        weight = 1

    [[menu.main]]
        name = "Blackwhale(OKD)"
        url = "https://console-openshift-console.apps.blackwhale.cloud.hancom.com/"
        weight = 2

# Markup configure section
# See https://gohugo.io/getting-started/configuration-markup/
[markup]
    defaultMarkdownHandler = "goldmark"
    [markup.goldmark.renderer]
        unsafe= true
    [markup.tableOfContents]
        startLevel = 2
        endLevel = 6
        ordered = false

[outputs]
    home = ["HTML", "RSS", "Algolia"]

# Algolia Search configure section
[outputFormats.Algolia]
    baseName = "algolia"
    mediaType = "application/json"
    isPlainText = true
    notAlternative = true

[params.algolia]
    vars = [
        "title",
        "summary",
        "content",
        "date",
        "publishdate",
        "description",
        "permalink",
        "keywords",
        "lastmod",
    ]
    params = [
        "tags",
        "categories",
    ]
```
{{% /tab %}}
{{< /tabs >}} 


### 3. exmaplesite 확인
- theme에 포함된 샘플사이트를 확인할수 있다. 
```
$ cd themes\hugo-theme-techdoc\exampleSite
$ hugo server --themesDir ../..
port 1313 already in use, attempting to use an available port
Start building sites … 
hugo v0.94.0-63B23660 windows/amd64 BuildDate=2022-03-10T09:46:36Z VendorInfo=gohugoio
WARN 2022/03/14 11:51:59 The "tweet" shortcode will soon require two named parameters: user and id. See "D:\Git\bluewhale\bluewhale-hugo\themes\hugo-theme-techdoc\exampleSite\content\sample\build-in-shortcodes.md:35:1"

                   | EN   
-------------------+------
  Pages            | 100
  Paginator pages  |   0
  Non-page files   |   0
  Static files     |   7
  Processed images |   0
  Aliases          |   1
  Sitemaps         |   1
  Cleaned          |   0

Built in 683 ms
Watching for changes in D:\Git\bluewhale\bluewhale-hugo\themes\hugo-theme-techdoc\{archetypes,exampleSite,layouts,package.json,static}
Watching for config changes in D:\Git\bluewhale\bluewhale-hugo\themes\hugo-theme-techdoc\exampleSite\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:2627/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

## 테마 변경

- [learn theme](https://themes.gohugo.io/themes/hugo-theme-learn/)  
- [learn 테마 참고1](https://learn.getgrav.org/17)  
- [learn 테마 참고2](https://learn.netlify.app/en/)  
- [learn 테마 folk repo](https://github.com/bluewhale-users/hugo-theme-learn)

### 1. 기존 테마 제거
```
// 모듈 제거 순서
$ git submodule deinit -f themes/hugo-theme-techdoc
$ rm -rf .git/modules/themes/hugo-theme-techdoc
$ git rm -f themes/hugo-theme-techdoc
```

```
$ git submodule deinit -f themes/hugo-theme-techdoc
Cleared directory 'themes/hugo-theme-techdoc'
Submodule 'themes/hugo-theme-techdoc' (https://github.com/thingsym/hugo-theme-techdoc.git) unregistered for path 'themes/hugo-theme-techdoc'

user@DESKTOP-1RAT70A MINGW64 /d/Git/bluewhale/bluewhale-hugo (master)
$ rm -rf .git/modules/themes/hugo-theme-techdoc

user@DESKTOP-1RAT70A MINGW64 /d/Git/bluewhale/bluewhale-hugo (master)
$ git rm -f themes/hugo-theme-techdoc
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory
rm 'themes/hugo-theme-techdoc'

```

### 2. 새로운 테마 설치
```
$ cd themes/
$ git clone https://github.com/matcornic/hugo-theme-learn.git
```

- 테마 exampleSite 확인
```
$ cd themes\hugo-theme-learn\exampleSite
$ hugo server --themesDir ../..
```

### 3. 빌드
```
$ hugo -t hugo-theme-learn
```


### 4. 오류
```
PS D:\Git\bluewhale\bluewhale-hugo> git submodule add -b master https://github.com/bluewhale-users/bluewhale.github.io.git public --force
A git directory for 'public' is found locally with remote(s):
  origin        https://github.com/bluewhale-users/bluewhale.github.io.git
If you want to reuse this local git directory instead of cloning again from
  https://github.com/bluewhale-users/bluewhale.github.io.git
use the '--force' option. If the local git directory is not the correct repo
or you are unsure what this means choose another name with the '--name' option.

.git/modules/ 폴더 삭제
```

### 5. front matter 
[spec](https://gohugo.io/content-management/front-matter/)



