---
title: "[Javascript] Array 인스턴스 메서드 "
description: "Array.prototype.reduce() "
author: cotes
date: 2024-07-05 14:00:00 +0900
categories: [Javascript]
tags: [javascript, reduce]  
pin: true
---





## reduce()

**`reduce()`** 메서드는 배열의 각 요소에 대해 주어진 리듀서 (reducer) 함수를 실행하고, 하나의 결과값을 반환한다.

``` javascript


const array = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue,
);

console.log(sumWithInitial);
// Expected output: 10

```



### 매개변수 

[`callback`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#callback)

배열의 각 요소에 대해 실행할 함수. 다음 네 가지 인수를 받는다.

- [`accumulator`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#accumulator)

  누산기는 콜백의 반환값을 누적하고 콜백의 이전 반환값 또는, 콜백의 첫 번째 호출이면서 `initialValue`를 제공한 경우에는 `initialValue`의 값인다

- [`currentValue`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#currentvalue)

  처리할 현재 요소.

- [`currentIndex`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#currentindex) Optional

  처리할 현재 요소의 인덱스. `initialValue`를 제공한 경우 0, 아니면 1부터 시작한ㄷ.

- [`array`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#array) Optional

  `reduce()`를 호출한 배열.



### [`reduce()` 작동 방식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#reduce_작동_방식)

다음의 예제를 보면서 생각해보기

jsCopy to Clipboard

```
[0, 1, 2, 3, 4].reduce(
  function (accumulator, currentValue, currentIndex, array) {
    return accumulator + currentValue;
  },
);
```

콜백은 4번 호출됩니다. 각 호출의 인수와 반환값은 다음과 같다

| `callback` | `accumulator` | `currentValue` | `currentIndex` | `array`           | 반환 값 |
| :--------- | :------------ | :------------- | :------------- | :---------------- | :------ |
| 1번째 호출 | `0`           | `1`            | `1`            | `[0, 1, 2, 3, 4]` | `1`     |
| 2번째 호출 | `1`           | `2`            | `2`            | `[0, 1, 2, 3, 4]` | `3`     |
| 3번째 호출 | `3`           | `3`            | `3`            | `[0, 1, 2, 3, 4]` | `6`     |
| 4번째 호출 | `6`           | `4`            | `4`            | `[0, 1, 2, 3, 4]` | `10`    |



`reduce()`가 반환하는 값으로는 마지막 콜백 호출의 반환값(`10`) 을 반환한다.