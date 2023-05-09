---
title: H5 Useful tips
index_img: >-
  https://rmt.dogedoge.com/fetch/fluid/storage/hello-fluid/cover.png?w=480&fmt=webp
author: Dylan
tags:
  - Tips
  - H5
math: true
mermaid: true
date: 2023-03-15 18:26:00
---
>H5 Useful tips

### Draw custom shapes with css
https://bennettfeely.com/clippy/

### Navigation List
https://www.figma.com/file/f6JxRIdSJ9YxWdsHrQC6lg/H5-BUTTON?node-id=0%3A1&t=216kIMNYg4jWsGzO-1

### Proto Generation for H5
protoc --plugin=./node_modules/.bin/protoc-gen-ts_proto --ts_proto_out=. ./src/service/<proto_name>.proto --ts_proto_opt=esModuleInterop=true --ts_proto_opt=env=browser