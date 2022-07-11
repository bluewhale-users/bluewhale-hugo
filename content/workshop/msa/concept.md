---
title: "Concept"
date: 2022-07-11T14:04:09+09:00
draft: true
---
[참고] https://dev.to/zachgoll/introduction-to-software-architecture-monolithic-vs-layered-vs-microservices-452

{{% notice info %}}
마이크로서비스는 소프트웨어가 잘 정의된 API를 통해 통신하는 소규모의 독립적인 서비스로 구성되어 있는 경우의 소프트웨어 개발을 위한 아키텍처 및 조직적 접근 방식입니다.  
이러한 서비스는 독립적인 소규모 팀에서 보유합니다.
마이크로서비스 아키텍처는 애플리케이션의 확장을 용이하게 하고 개발 속도를 앞당겨 혁신을 실현하고 새로운 기능의 출시 시간을 단축할 수 있게 해 줍니다.
{{% /notice %}}

## 모놀리식 아키텍처 VS 마이크로서비스 아키텍처 

![마이크로서비스](./architecture.png?width=400pt&classes=border) 

## Monolithic Architecture
전통적인 모놀로식 아키텍처가 비효율적으로 보일 수 있지만 실제로 개발중인 애플리케이션이 충분히 복잡하지 않다면 마이크로서비스 아키텍처의 이점을 확인하기는 쉽지 않다. 
비교적 간단한 아키텍처의 경우 충분히 활용 가능한 솔루션이라고 할 수 있다.

따라서 모놀로딕 아키텍처로 시작하여 마이크로 서비스 아키텍처로 리팩토링하는것이 효율적인 개발 방법일수도 있다. 

### 장점
- 손쉬운 배포 : 단일 실행파일 또는 디렉토리로 작성되어 배포가 쉽다. 
- 개발 : 단일 코드베이스로 구성되어 애플리케이션 개발이 쉽다. 
- 성능 : 단일 API를 사용하여 마이크로서비스의 여러 API가 수행하는 결과와 동일한 기능을 수행한다. 
- 테스트 간소화 : 중앙집중식 구성으로 분산된 환경보다 End-TO-End 테스트를 더 빠르게 수행할 수 있다. 
- 디버깅 : 모든 코드가 한곳에 있으므로 요청을 트랙킹해 문제를 찾기 더 쉽다. 

### 애플리케이션 구조
아래의 코드를 통해 monolithic 구조를 살펴보자.

[monolithic architecture example github] https://github.com/zachgoll/monolithic-architecture-example-app

이 코드에서 확인 가능한것은 애플리케이션간의 구분이 없다는것이다. 
app.js에서 데이터베이스, 서버 및 API 엔드포인트에 대한 연결을 확인할 수 있다. 

``` js
const express = require("express");
const app = express();
const mongoose = require("mongoose");
const cors = require("cors");
const bodyParser = require("body-parser");

// This will allow our presentation layer to retrieve data from this API without
// running into cross-origin issues (CORS)
app.use(cors());
app.use(bodyParser.json());

// ============================================
// ==========  DATABASE CONNECTION  ===========
// ============================================
// Connect to running database
mongoose.connect(
  `mongodb://${process.env.DB_USER}:${process.env.DB_PW}@127.0.0.1:27017/monolithic_app_db`,
  { useNewUrlParser: true }
);

// User schema for mongodb
const UserSchema = mongoose.Schema(
  {
    name: { type: String },
    email: { type: String },
  },
  { collection: "users" }
);

// Define the mongoose model for use below in method
const User = mongoose.model("User", UserSchema);

function getUserByEmail(email, callback) {
  try {
    User.findOne({ email: email }, callback);
  } catch (err) {
    callback(err);
  }
}

// set the view engine to ejs
app.set("view engine", "ejs");

// index page
app.get("/", function (req, res) {
  res.render("home");
});

// ============================================
// ============  API ENDPOINT  ================
// ============================================
app.post("/register", function (req, res) {
  const newUser = new User({
    name: req.body.name,
    email: req.body.email,
  });

  newUser.save((err, user) => {
    res.status(200).json(user);
  });
});

// ============================================
// ==============  SERVER =====================
// ============================================
app.listen(8080);
console.log("Visit app at http://localhost:8080");
```

이 모놀리딕 애플리케이션이 확장하기 시작할 경우 빠르게 코드는 엉망이 될 것이다. 
이 단계에서 대부분 마이크로서비스 아키텍처로의 전환을 선택하지만, 리팩토링을 통하여 계층화된 아키텍처로 바꾸는것을 다른 하나의 옵션으로 고민해 볼 수 있다. 

계층화된 아키텍처는 애플리케이션을 일반적으로 다음과 같은 레이어들로 분할할 수 있다. 

1. 프리젠테이션 계층
2. 비지니스 계층
3. 데이터 액세스 계층


[monolithic layered architecture example github] https://github.com/zachgoll/layered-architecture-example-app