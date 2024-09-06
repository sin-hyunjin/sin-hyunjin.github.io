---
title: "[React] Hooks "
description: "리액트정리 2탄 Hooks 정리 "
author: cotes
date: 2024-07-05 17:00:00 +0900
categories: [React, Hooks]
tags: [react, set]
pin: true
---
<details>
  <summary><span style="font-size: 24px; font-style: italic;">리액트 복습 및 정리하기</span></summary>
  <ul>
   <li><a href="/posts/react-es6/">리액트 정리1탄 (ES6, Props)</a></li>
    <li><a href="/posts/react-hooks/">리액트 정리2탄 (Hooks)</a></li>
  </ul>
</details>

### useState Hook

**useState**는 함수형 컴포넌트에서 상태를 관리하는 데 사용됨 이 Hook을 사용하면 상태 변수를 선언하고 해당 변수를 업데이트하는 함수를 제공받고 초기 상태 값을 인자로 받아 초기화하며, setState 함수를 통해 상태를 변경할 수 있다.

``` javascript


import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

export default Counter;
```

### useEffect Hook

**useEffect**는 함수형 컴포넌트에서 side effect를 처리하는 데 사용된다. 컴포넌트가 렌더링될 때마다 특정 작업을 수행하거나, props 또는 state의 변경에 따라 추가적인 작업을 수행할 수 있다.

```javascript


import React, { useEffect, useState } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // 빈 배열을 넘겨 초기 렌더링 시 한 번만 실행

  return (
    <div>
      {data ? (
        <ul>
          {data.map(item => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
};

export default DataFetcher;
```

### useReducer Hook

**useReducer**는 복잡한 상태 관리 로직을 개선하기 위해 사용되며 이 Hook을 사용하여 상태와 그 상태를 업데이트하는 액션을 처리하는 reducer 함수를 함께 사용하여 상태를 업데이트할 수 있다.

``` javascript


import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
};

export default Counter;
```

### useMemo Hook

**useMemo**는 함수의 결과 값을 메모이제이션하여 성능을 최적화하는 데 사용된다, 의존성 배열을 지정하여 해당 값이 변경될 때만 함수를 다시 계산한다.

``` javascript


import React, { useMemo, useState } from 'react';

const ExpensiveComponent = ({ count }) => {
  const expensiveFunction = useMemo(() => {
    console.log('Calculating...');
    let result = 0;
    for (let i = 0; i < count * 1000000; i++) {
      result += i;
    }
    return result;
  }, [count]);

  return <div>Expensive calculation result: {expensiveFunction}</div>;
};

const MemoExample = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <ExpensiveComponent count={count} />
    </div>
  );
};

export default MemoExample;
```

### useCallback Hook

**useCallback**은 메모이제이션된 콜백 함수를 반환하여 자식 컴포넌트에 전달할 때 불필요한 재렌더링을 방지하는 데 사용된다,

``` javascript

import React, { useState, useCallback } from 'react';

const CallbackExample = () => {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
};

export default CallbackExample;
```

### useRef Hook

**useRef**는 함수형 컴포넌트에서 ref를 생성하거나 DOM 노드에 접근하는 데 사용된다.

``` javascript

import React, { useRef } from 'react';

const FocusInput = () => {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
};

export default FocusInput;
```

### Custom Hooks

**Custom Hooks**는 반복되는 로직을 함수로 추상화하여 재사용할 수 있는 Hook . 다양한 컴포넌트에서 동일한 로직을 사용할 때 Custom Hook을 만들어 사용하면 코드의 재사용성과 가독성을 높일 수 있다.

``` javascript

import { useState, useEffect } from 'react';

const useCustomHook = (initialValue) => {
  const [value, setValue] = useState(initialValue);

  useEffect(() => {
    console.log('Value changed:', value);
  }, [value]);

  const handleChange = (newValue) => {
    setValue(newValue);
  };

  return [value, handleChange];
};

export default useCustomHook;
```

