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
<summary><span style="font-size: 24px;font-style: italic;">리액트 복습 및 정리하기</span>
</summary>
  • <a href="./2024-07-06-react-es6.md"> 리액트 정리1탄 (ES6 , Props) </a>   </br>
   • <a href="./2024-07-06-react-hooks.md"> 리액트 정리2탄 (Hooks)</a>




### useState Hook

**useState**는 함수형 컴포넌트에서 상태를 관리하는 데 사용됩니다. 이 Hook을 사용하면 상태 변수를 선언하고 해당 변수를 업데이트하는 함수를 제공받습니다. 초기 상태 값을 인자로 받아 초기화하며, setState 함수를 통해 상태를 변경할 수 있습니다.

```
jsx

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

**useEffect**는 함수형 컴포넌트에서 side effect를 처리하는 데 사용됩니다. 컴포넌트가 렌더링될 때마다 특정 작업을 수행하거나, props 또는 state의 변경에 따라 추가적인 작업을 수행할 수 있습니다.

```
jsx

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

**useReducer**는 복잡한 상태 관리 로직을 개선하기 위해 사용됩니다. 이 Hook을 사용하여 상태와 그 상태를 업데이트하는 액션을 처리하는 reducer 함수를 함께 사용하여 상태를 업데이트할 수 있습니다.

```
jsx

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

**useMemo**는 함수의 결과 값을 메모이제이션하여 성능을 최적화하는 데 사용됩니다. 의존성 배열을 지정하여 해당 값이 변경될 때만 함수를 다시 계산합니다.

```
jsx

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

**useCallback**은 메모이제이션된 콜백 함수를 반환하여 자식 컴포넌트에 전달할 때 불필요한 재렌더링을 방지하는 데 사용됩니다.

```
jsx

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

**useRef**는 함수형 컴포넌트에서 ref를 생성하거나 DOM 노드에 접근하는 데 사용됩니다.

```
jsx

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

**Custom Hooks**는 반복되는 로직을 함수로 추상화하여 재사용할 수 있는 Hook입니다. 다양한 컴포넌트에서 동일한 로직을 사용할 때 Custom Hook을 만들어 사용하면 코드의 재사용성과 가독성을 높일 수 있습니다.

```
jsx

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

이제 각 Hook에 대한 기본 개념과 예제 코드를 제공해드렸습니다. 이를 참고하여 React에서 Hook을 활용하는 방법을 익히시기 바랍니다!





결과값도 같이 적어주고 주석도 해줘



ChatGPT

알겠습니다! 각 Hook에 대한 예제 코드와 결과값, 그리고 주석을 포함하여 정리해드리겠습니다.

### useState Hook

**useState**는 함수형 컴포넌트에서 상태를 관리하는 데 사용됩니다. 이 Hook을 사용하면 상태 변수를 선언하고 해당 변수를 업데이트하는 함수를 제공받습니다. 초기 상태 값을 인자로 받아 초기화하며, setState 함수를 통해 상태를 변경할 수 있습니다.

```
jsx

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

- **결과값**: 화면에 "Count: 0"과 "Increment" 버튼이 표시됩니다. 버튼을 클릭할 때마다 Count 값이 증가합니다.

### useEffect Hook

**useEffect**는 함수형 컴포넌트에서 side effect를 처리하는 데 사용됩니다. 컴포넌트가 렌더링될 때마다 특정 작업을 수행하거나, props 또는 state의 변경에 따라 추가적인 작업을 수행할 수 있습니다.

```
jsx

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

- **결과값**: 초기 렌더링 시 "Loading..."이 표시되며, 데이터를 불러오면 리스트가 표시됩니다.

### useReducer Hook

**useReducer**는 복잡한 상태 관리 로직을 개선하기 위해 사용됩니다. 이 Hook을 사용하여 상태와 그 상태를 업데이트하는 액션을 처리하는 reducer 함수를 함께 사용하여 상태를 업데이트할 수 있습니다.

```
jsx

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

- **결과값**: 화면에 "Count: 0", "Increment" 버튼, "Decrement" 버튼이 표시됩니다. 버튼을 클릭할 때마다 Count 값이 증가 또는 감소합니다.

### useMemo Hook

**useMemo**는 함수의 결과 값을 메모이제이션하여 성능을 최적화하는 데 사용됩니다. 의존성 배열을 지정하여 해당 값이 변경될 때만 함수를 다시 계





겨



ChatGPT

죄송합니다. 이전에 응답을 마치지 않고 종료된 것 같습니다. 다시 시작하겠습니다.

### useMemo Hook

**useMemo**는 함수의 결과 값을 메모이제이션하여 성능을 최적화하는 데 사용됩니다. 의존성 배열을 지정하여 해당 값이 변경될 때만 함수를 다시 계산합니다.

```
jsx

import React, { useMemo, useState } from 'react';

const ExpensiveComponent = ({ count }) => {
  const expensiveCalculation = useMemo(() => {
    console.log('Calculating...');
    let result = 0;
    for (let i = 0; i < count; i++) {
      result += i;
    }
    return result;
  }, [count]);

  return (
    <div
```





결과값도



ChatGPT

죄송합니다. 이전에 응답을 마치지 않고 종료된 것 같습니다. 다시 시작하겠습니다.





결과값도 코드로해줘



ChatGPT

네, 이해했습니다. useMemo Hook의 예제 코드에 대한 결과값을 함께 설명드리겠습니다.

### useMemo Hook

**useMemo**는 함수의 결과 값을 메모이제이션하여 성능을 최적화하는 데 사용됩니다. 의존성 배열을 지정하여 해당 값이 변경될 때만 함수를 다시 계산합니다.

```
jsx

import React, { useMemo, useState } from 'react';

const ExpensiveComponent = ({ count }) => {
  const expensiveCalculation = useMemo(() => {
    console.log('Calculating...');
    let result = 0;
    for (let i = 0; i < count; i++) {
      result += i;
    }
    return result;
  }, [count]);

  return (
    <div>
      <p>Result: {expensiveCalculation}</p>
    </div>
  );
};

const App = () => {
  const [count, setCount] = useState(5);

  const incrementCount = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <button onClick={incrementCount}>Increment Count</button>
      <ExpensiveComponent count={count} />
    </div>
  );
};

export default App;
```

### 결과값

- 초기 렌더링 시:
  - "Calculating..."이 콘솔에 표시됩니다.
  - 화면에 "Result: 10"이 표시됩니다. (count 값이 5일 때, 0부터 4까지의 합인 10)
- 버튼을 클릭하여 Increment Count 버튼을 클릭할 때:
  - "Calculating..."이 다시 콘솔에 표시됩니다.
  - 화면에 "Result: 15"가 표시됩니다. (count 값이 6일 때, 0부터 5까지의 합인 15)