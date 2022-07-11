---
title: "Msa"
date: 2022-07-11T14:04:15+09:00
draft: true
---

[netflex microservice] https://netflixtechblog.com/tagged/microservices

{{% notice info %}}
마이크로서비스는 소프트웨어가 잘 정의된 API를 통해 통신하는 소규모의 독립적인 서비스로 구성되어 있는 경우의 소프트웨어 개발을 위한 아키텍처 및 조직적 접근 방식입니다.  
이러한 서비스는 독립적인 소규모 팀에서 보유합니다.
마이크로서비스 아키텍처는 애플리케이션의 확장을 용이하게 하고 개발 속도를 앞당겨 혁신을 실현하고 새로운 기능의 출시 시간을 단축할 수 있게 해 줍니다.
{{% /notice %}}

## 모놀리식 아키텍처 VS 마이크로서비스 아키텍처
모놀리식 아키텍처의 경우 모든 프로세스가 긴밀하게 결합되고 단일 서비스로 실행됩니다. 따라서 애플리케이션의 한 프로세스에 대한 수요가 급증하면 해당 아키텍처 전체를 확장해야 합니다. 코드 베이스가 증가하게 되면 모놀리식 애플리케이션의 기능을 추가하거나 개선하기가 더 복잡해집니다.  
그리고 이러한 복잡성으로 인해 실험에 제한을 받고 새로운 아이디어를 구현하기가 어려워집니다. 종속 관계를 이루며 긴밀하게 결합된 많은 프로세스로 인해 단일 프로세스의 실패로 인한 영향이 증가함에 따라 모놀리식 아키텍처는 애플리케이션 가용성에 대한 위험을 가중시킵니다.

![마이크로서비스](introduction/microservices.jpg#floatright)

마이크로서비스 아키텍처의 경우, 애플리케이션이 독립적인 구성 요소로 구축되어 각 애플리케이션 프로세스가 서비스로 실행됩니다. 이러한 서비스는 경량 API를 사용하여 잘 정의된 인터페이스를 통해 통신합니다. 서비스는 비즈니스 기능을 위해 구축되며 서비스마다 한 가지 기능을 수행합니다. 서비스가 독립적으로 실행되기 때문에 애플리케이션의 특정 기능에 대한 수요를 충족하도록 각각의 서비스를 업데이트, 배포 및 확장할 수 있습니다.

[출처] https://aws.amazon.com/ko/microservices/


<!-- {{< rawhtml >}}
<div class="map-responsive">
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3169.563794435667!2d127.11039003253148!3d37.40014688566732!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357ca7019af06e6d%3A0x6645947f52117e91!2z7ZWc6riA6rO87Lu07ZOo7YSw6re466O5!5e0!3m2!1sko!2skr!4v1657256591416!5m2!1sko!2skr" width="300" height="200" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
</div>
{{< /rawhtml >}}  -->

[bluewhale-users](https://bluewhale-users.github.io/ko/)