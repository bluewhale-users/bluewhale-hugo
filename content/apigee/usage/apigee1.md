---
title: "Apigee1 : 소개"
date: 2022-03-29T13:44:42+09:00
weight: 41
draft: false
---

## Apigee 소개

- [Apigee 기술문서](https://docs.apigee.com/)  
- [Apigee 문서](https://cloud.google.com/apigee/docs)  
- [Choosing between service management and API management](https://www.youtube.com/watch?v=1FV0Vv-me08)

### 1. 요약
{{% notice info %}}
Apigee는 API 개발 및 관리를 위한 플랫폼입니다. 
Apigee는 프록시 레이어와 함께 서비스를 전면에 내세워 백엔드 서비스 API의 추상화 또는 퍼사드를 제공하고 보안, 비율 제한, 할당량, 분석 등을 제공합니다.
{{% /notice %}}


### 2. Apigee 사용 목적
- 전체 API 수명 주기 기능으로 API 프로그램 빌드 및 확장
- 유연한 개발자 포털 옵션으로 API 사용 촉진
- 전체 API 가치 사슬에서 활용 가능한 분석 정보 확보
- API 제품으로 수익을 창출하고 디지털 자산의 비즈니스 가치 극대화


### 3. Apigee Architecture
- Apigee 서비스: API 프록시를 생성, 관리, 배포하는 데 사용하는 API입니다.
- Apigee 런타임: Google이 Kubernetes 클러스터에서 유지관리하는 컨테이너화된 런타임 서비스 집합입니다. 모든 API 트래픽이 통과되어 이러한 서비스에 의해 처리됩니다. 
- GCP[^footnote1] 서비스: ID 관리, 로깅, 분석, 측정항목, 프로젝트 관리 기능을 제공합니다.
- 백엔드 서비스: 앱에서 API 프록시의 데이터에 대한 런타임 액세스를 제공하기 위해 사용합니다
{{< figure src="/apigee/apigee-start_1.jpg" title="Apigee high-level overview" >}}
[출처] https://cloud.google.com/apigee/docs/api-platform/get-started/what-apigee

### 4. Architecture Detail
- 비공개 피어링 네트워크를 통해 Cloud 프로젝트와 Google 서비스 간의 연결을 보여주는 세부적인 그림입니다. 
{{< figure src="/apigee/apigee-start_2.jpg" title="Apigee architecture">}}
[출처] https://cloud.google.com/apigee/docs/api-platform/get-started/what-apigee

### 5. Apigee 유형
- Apigee
  - Apigee가 환경을 유지관리하는 호스팅된 SaaS 버전으로, 서비스를 빌드하고 해당 서비스에 API를 정의하는 데 집중할 수 있습니다.
- Apigee Hybrid
  - 온프레미스 또는 선택한 클라우드 제공업체에 설치된 런타임 영역과, Apigee 클라우드에서 실행되는 관리 영역으로 구성된 하이브리드 버전입니다. 이 모델에서는 사용자의 자체 기업 승인을 받은 경계 내에서 API 트래픽 및 데이터가 제한됩니다.

### 6. Apigee 서비스 이용시 이점
- Apigee를 사용하면 서비스 구현에 관계없이 모든 서비스에서 명확하게 정의되고 일관된 API를 통해 서비스에 안전하게 액세스할 수 있습니다. 일관된 API를 사용하여 다음 이점을 활용할 수 있습니다.
  - 앱 개발자가 서비스를 쉽게 사용할 수 있습니다.
  - 공개 API에 영향을 미치지 않고 백엔드 서비스 구현을 변경할 수 있습니다.
  - Apigee에 내장된 분석, 개발자 포털, 기타 기능을 활용할 수 있습니다.

### 서비스 관리와 API 관리 차이
#### Overview
- Service management
  - 서비스 관리는 서비스 메시로 수행됩니다.
  - 서비스 간 통신을 관리하며 서비스 정책 또는 원격 측정에 대한 전반적인 서비스를 처리하는 데 중점을 둡니다.
- API management
  - API 관리는 일반적으로 API 플랫폼으로 수행됩니다. 
  - API 수명 주기 관리에 관한 모든것이며, API 게시, 소비, 거버넌스 및 소비자의 API 사용 분석 수신에 맞춰져 있습니다.  

#### Modernization journey(기업의 현대화)
- Service management와 API management 2가지 요소는 기업 현대화의 필수 요소입니다. 
- 문제는 어느것을 선택해야 하는것이 아니라 언제 어디서 선택하느냐 하는것입니다. 
- 현대화 과정의 현재 위치에 따라 둘 중 하나를 선택할 수 있습니다. 
- 또는 하나의 사용 사례에 대해 API 관리를 선택하고 다른 사용 사례를 사용하여 비지니스의 다른 부분에 대해 서비스 관리를 선택할 수 있습니다. 

#### Modernization journey의 목표
- 클라우드 네이티브 기술로 애플리케이션을 현대화하여 소프트웨어를 더 빠르게 제공
- 개발자, 파트너 및 고객에게 고유한 방법을 제공하여 비지니스를 혁신 

두 가지 목표를 모두 달성하려면 서비스 관리와 AIP 관리가 모두 필요합니다. 


#### 서비스 관리 또는 API 관리를 선택할 위치와 시기를 결정할수 있는 시나리오
- Standardize service policies for an internal platform
  - 조직이 표준화돤 보안정책 및 제어에 대한 요구 사항을 가진 내부 플랫폼을 구축하려고 할 때

use cases  
- Standardize service polices for an internal platform  
조직이 표준화된 보안정책 및 제어에 대한 요구 사항을 가진 내부 플랫폼을 구축하고 있을때
Service management 계층은 해당 플랫폼 내에서 트래픽을 보호하고 제어하는 데 필요한 모든 기능을 제공합니다.

- Monitor services and set Service-level Objectives(SLOs)  
다음으로 SRE팀은 해당 플랫폼 내 서비스의 상태와 성능을 모니터링하려고 합니다. 
이 시나리오에서 서비스 관리는 SLO를 설정하고 경고를 받을수 있도록 메트릭, 로그 및 추적을 팀에 제공할 수 있습니다. 

- Configure networking components for services communication  
그리고 팀의 네트워크 운영자가 하이브리드 또는 다중 클라우드 상황에서 서비스가 클러스터간 통신할 수 있도록 네트워킹
구성해야 할 경우에는 어떻게 할까요?
서비스 관리는 이러한 환경 및 구성 요소에서 네트워킹을 표준화하는 방법을 제공합니다. 
이제 이 플랫폼이 기업내의 사업부에서 소유하고 있다록 상상해 보십시오

- Build a shared service model internally  
이들은 다른 사업부가 이러한 표준화된 서비스 중 일부를 API로 발견하고 재사용할 수 있는 공유 서비스 모델을 설정하기를
원할 수 있습니다. 
이 경우 목표는 사용 가능한 API와 사용 방법에 대해 신뢰 영역 외부에 있는 다른 팀에 쉽게 가시성을 제공합는 것입니다. 
API management platform은 이러한 프로세스를 관리하는 좋은 방법입니다. 
이러한 API를 다른 팀에 노출하는 매커니즘을 제공하고, 이러한 서비스에 대한 액세스를 제공하고, 분석을 통해
API 사용량을 측정하는 도구를 제공합니다. 
여기에서 이 조직은 이제 제 3자 파트너와 개발자를 결합하려는 시점에 있습니다. 
이는 오픈 뱅킹과 같은 업계 관행을 따르거나 비지니스 모델을 새로운 채널로 확장하기 위한 것일 수 있습니다. 
마지막 사용 사례와 유사하게 API 관리 플랫폼ㅇ르 사용하면 조직 외부에 해당 서비스를 안전하게 노출하고 도구를 제공하며
손쉬운 온보딩 및 액세를 제공할 수 있습니다. 

- Monetize APIs  
이제 이러한 모든 이해 관계자에게 해당 API에 대한 액세스 권한을 부여했으므로 API가 어떻게 사용되는지 확인하고 잠재적으로
일부 수익창출 기회를 탐색할 수 있습니다.
이것은 API management platform에 매우 적합한 시나리오입니다. 
API 소비 및 성장에 대한 가시성을 확보하고 어떤 API가 가치가 있는지 판단하고, 제3자에게 비용을 청구하려는 API주변에 수익창출 모델을 배치 할 수 있습니다. 

이 둘을 함께 사용하여 구축중인 플랫폼에 대해 서로 다른 기능을 수행하도록 할 수 있습니다. 

Service to service communicatin : Service management(Anthos Service Mesh)
> https://cloud.google.com/anthos/service-mesh

Sharing APIs outside your domain of trust : API management(Apigee)
> https://cloud.google.com/apigee


### 7. Apigee 가격 정책
[참고](https://cloud.google.com/apigee/pricing)

평가		                     | 표준			               | 엔터프라이즈              | 엔터프라이즈 플러스
:------	                        |:-------			           |:------                  |:------
월별 API 호출 100,000회          | 연간 API 호출 1억 8,000만 회	 | 연간 API 호출 12억 회    | 연간 API 호출 120억 회
환경 2개                         | 조직 1개 및 환경 5개			 | 조직 2개 및 환경 10개    | 조직 6개 및 환경 30개
애널리틱스 보고서 30일            | 애널리틱스 보고서 30일		   | 애널리틱스 보고서 3개월  | 애널리틱스 보고서 14개월
런타임 SLA 없음                  | 99% 런타임 SLA			     | 99.9% 런타임 SLA        | 99.99% 런타임 SLA
유료 서비스로의 마이그레이션 불가  |  			                   | 하이브리드 배포 지원     | 하이브리드 배포 지원
60일 후 평가 종료                |    	                         |                        | 엔터프라이즈 플러스

#### 8. Service Level Agreement (SLA)  
[참고](https://cloud.google.com/apigee/sla)
Covered Service		                     | Monthly Uptime Percentage		                
:------	                                |:-------			            
Apigee Standard                         | >= 99%		  
Apigee Enterprise                       | >= 99.99% for environments provisioned in 2 or more Regions (i.e., with the purchase of Additional Region / Distributed Network) with a dual-region, multi-regional, or global Cloud KMS encryption key, or >= 99.9% for all other environments	    
Apigee Enterprise Plus                  | >= 99.99% for environments provisioned in 2 or more Regions with a dual-region, multi-regional, or global Cloud KMS encryption key, or >= 99.9% for all other environments

 

[^footnote1]: Google Cloud Platform은 전 세계 사용자들에게 구글 내부 인프라를 사용할 수 있도록 해 주 는 제품 모음입니다. 이 모음에는 구글 Compute Engine을 통한 주문형 가상 머신이나 Google Cloud Storage를 통한 파일 저장용 오브젝트 스토리지같이 다른 클라우드 서비스 업체에서도 공통적으로 제공하는 여러 기능이 포함되어 있습니다. 또한, Bigtable, Cloud Datastore 또는 Kubernetes와 같은 구글이 만든 고급 기술에 대한 API도 포함하고 있습니다. 


