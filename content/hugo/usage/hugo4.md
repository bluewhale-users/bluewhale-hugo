---
title: "Hugo4 : css 스타일 참조"
date: 2022-03-22T11:24:21+09:00
draft: true
weight: 44
---

## css 파일 추가

### 1. config.toml 파일 수정
```
[params]
  ...
  custom_css = ["css/custom.css"]
  ...
```

### 2. css 파일 추가
```
static/css/custom.css 파일 추가
```

- custom.css
```
img[src$='#floatleft']
{
	float:left;
}

img[src$='#floatright']
{
	float:right;
}

figure.floatright {
	max-width: 30%;
	width: auto\9*0.3; /* ie8 */
	height: auto;
	float: right;
}

figure.floatleft {
	max-width: 30%;
	width: auto\9*0.3; /* ie8 */
	height: auto;
	float: left;
}
```

### 3. layouts/partials/header.html 수정
```
....
{{ range .Site.Params.custom_css -}}
    ...
    <link rel="stylesheet" href="{{ . | absURL }}">
{{- end }}
....
```

### 3. css 스타일 참조(그림 정렬)


{{< tabs >}}
{{% tab name="기본 정렬" %}}
``` 
{{< figure src="/cicd/tutorial4_4.jpg" >}}
```
{{% /tab %}}
{{% tab name="왼쪽 정렬" %}}
``` 
{{< figure src="/cicd/tutorial4_4.jpg#floatleft" >}}
```
{{% /tab %}}
{{< /tabs >}}

{{< figure src="/cicd/tutorial4_4.jpg" >}}
{{< figure src="/cicd/tutorial4_4.jpg#floatleft" >}}