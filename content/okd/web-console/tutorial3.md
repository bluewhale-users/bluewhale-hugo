---
title: "Tutorial3 : 프로젝트 삭제"
date: 2022-04-11T09:33:10+09:00
draft: false
weight: 43
---

### 1. 프로젝트 삭제

- 삭제할 Application을 선택한다. 
{{< figure src="/web-console/tutorial3_1.jpg" >}}

- 마우스 우클릭을 하여 'Delete Application'을 선택한다. 
{{< figure src="/web-console/tutorial3_2.jpg" >}}

- 확인용 app 이름을 타이핑해 넣는다.  
  (연결된 모든 Deployments, Routes, Builds, Pipelines, Storage/PCVs, Secret 및 ConfigMap 이 삭제됩니다.)
{{< figure src="/web-console/tutorial3_3.jpg" >}}

- 삭제 완료
{{< figure src="/web-console/tutorial3_4.jpg" >}}


{{% notice info %}}
이 단계를 거치지 않고 리소스를 부분적으로 삭제하게 되면 남아 있는 리소스들을 수동으로 삭제해야 한다.
{{% /notice %}}