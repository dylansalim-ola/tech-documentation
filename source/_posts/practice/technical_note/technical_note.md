---
title: Technical note
index_img: >-
  /images/workflow.png
author: Dylan
tags:
  - Technical note
math: true
mermaid: true
date: 2023-03-27 11:48:00
---

## H5 Proto to Typescript
```bash
protoc --plugin=./node_modules/.bin/protoc-gen-ts_proto --ts_proto_out=. ./src/service/recharge_agent.proto --ts_proto_opt=esModuleInterop=true --ts_proto_opt=env=browser
```

## Mobx generation
```bash
flutter pub run mobx_bin:gen -s banban_base/bbroom/lib/src/lucky_wheel/store/lucky_wheel_store.dart
```

## Reload
```bash
curl --location --request POST 'http://vk.sgola.cc/go/Payment/InternalCreditAccount' \
--header 'Content-Type: application/json' \
--data-raw '{"userID”:”112684”, type":"gold_normal","operation":"income","amount":"99999","expiry":"2023-10-01T00:00:00Z","trxType":"internal_iap","trxID":"1","trxUniqueKey":"","subject":"加钱","opDetail":{"scenario":"test","extra":{}}}'
```