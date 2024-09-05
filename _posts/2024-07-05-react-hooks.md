---
title: "[React] Hooks "
description: "리액트정리 2탄 Hooks 정리 "
author: cotes
date: 2024-07-05 17:00:00 +0900
categories: [React, Hooks ]
tags: [react, set]
pin: true
---
<details> 
<summary><span style="font-size: 24px;font-style: italic;">리액트 복습 및 정리하기</span>
</summary>
  • <a href="./2024-07-06-react-es6.md"> 리액트 정리1탄 (ES6 , Props) </a>   </br>
   • <a href="./2024-07-06-react-hooks.md"> 리액트 정리2탄 (Hooks)</a>




## React Hooks란?

Hooks는 함수형 컴포넌트에서 **상태(state)**와 **생명주기(lifecycle)** 관련 기능을 사용할 수 있게 해주는 기능이다. 이전에는 클래스형 컴포넌트에서만 가능했던 기능을, Hooks 덕분에 함수형 컴포넌트에서도 사용할 수 있게 되었다.



## 주요 Hooks

1. **useState**
   컴포넌트 내에서 상태를 관리할 수 있게 해주는 Hook이다. `useState`는 상태 변수와 그 상태를 업데이트할 수 있는 함수를 반환하며, 컴포넌트가 다시 렌더링될 때도 상태가 유지된다.

   ```
   javascript
   코드 복사
   const [count, setCount] = useState(0);
   
   const increment = () => setCount(count + 1);
   ```

2. **useEffect**
   **컴포넌트의 생명주기**와 관련된 작업(예: API 호출, DOM 업데이트 등)을 처리할 수 있게 해주는 Hook이다. 컴포넌트가 **렌더링될 때**와 **변경될 때** 특정 작업을 실행할 수 있다. 또한, 리턴 함수로 **정리 작업(cleanup)**을 할 수 있다.

   ```
   javascript
   코드 복사
   useEffect(() => {
     console.log("컴포넌트가 렌더링됨");
   
     return () => {
       console.log("컴포넌트가 언마운트됨");
     };
   }, []);
   ```

3. **useContext**
   `useContext`는 컴포넌트 간에 **데이터를 손쉽게 공유**할 수 있게 해주는 Hook이다. `Context`는 부모 컴포넌트에서 자식 컴포넌트로 프롭스를 넘기는 대신, 전역적으로 데이터를 관리하는 데 사용한다.

   ```
   javascript
   코드 복사
   const MyContext = React.createContext();
   
   const App = () => {
     return (
       <MyContext.Provider value={"Hello"}>
         <ChildComponent />
       </MyContext.Provider>
     );
   };
   
   const ChildComponent = () => {
     const value = useContext(MyContext);
     return <div>{value}</div>;
   };
   ```

4. **useRef**
   `useRef`는 DOM 요소에 접근하거나 값이 변경되어도 **렌더링을 발생시키지 않는** 변수를 저장하는 데 사용된다. DOM 요소에 직접 접근하여 포커스를 주거나 값을 저장하는 데 유용하다.

   ```
   javascript
   코드 복사
   const inputRef = useRef(null);
   
   const focusInput = () => {
     inputRef.current.focus();
   ```