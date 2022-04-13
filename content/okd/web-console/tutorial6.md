---
title: "Tutorial6 : manifest를 이용한 배포"
date: 2022-04-13T09:18:31+09:00
draft: true
---

- [manifest github](https://github.com/bluewhale-users/okd-tutorial3)

### 1. 


oc new-app centos/mongodb-26-centos7 -e MONGODB_USER=admin -e MONGODB_DATABASE=mongo_db -e MONGODB_PASSWORD=secret -e MONGODB_ADMIN_PASSWORD=super-secret


oc set env deployment/nodejs-sample MONGO_URL='mongodb://admin:secret@172.30.93.87:27017/mongo_db'