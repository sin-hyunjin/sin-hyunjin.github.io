---
title: "[Vite] 프로젝트 절대 경로 설정하기"
description: "상대경로의 가독성 문제 및 프로젝트 절대 경로 설정하기"
author: cotes
date: 2024-06-05 17:00:00 +0900
categories: [Vite]
tags: [vite, set]
pin: true
---



## 절대 경로 필요성 

개발을 하다보니 import 경로가 길어지면서 불편함이 생겼다. 특히, 파일구조가 복잡해질수록 상대 경로로 파일을 import하는 것이 번거러워 졌다. 

예를 들어,

```javascript
import Component from '../../../../components/Component.jsx'
```

이렇게  상대 경로를 한눈에 이해하기가 어렵고, 경로가 잘못된 가능성이 높아져지기 때문이다.



## ✔ Vite에서 절대 경로 설정하기 

Vite 프로젝트에서 절대 경로를 설정하려면 `vite.config.js` 파일을 수정하면 된다.

![image-20240605230412211](../images/2024-06-30-vite-absolute path/image-20240605230412211.png)

나의 경우 이런 폴더구조로 만들어져 있다.

```javascript
// vite.config.js

import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [
      { find: "@", replacement: "/src" },
      { find: "@components", replacement: "/src/components" },
      { find: "@constants", replacement: "/src/constants" },
      { find: "@mocks", replacement: "/src/mocks" },
      { find: "@utils", replacement: "/src/utils" },
    ]}
})

```

alias 에 배열로, 찾을 경로와 바꿀 경로를 바꿔주면 된다.

추가로 여러개의 alias를 설정하고 싶다면, `resolve.alias` 객체에 추가하면 된다.



## ✔ 결과

``` javascript
import Component from '@components/Component.jsx';
import { myUtil } from '@utils/Util';
```

이렇게  절대 경로로 사용할수 있게 되었다 



> Vite 프로젝트에서 절대 경로를 설정하면서  코드의 가독성과, 상대 경로의 불편함을 해소할 수  있었다.



