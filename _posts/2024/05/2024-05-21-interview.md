---
title: "프론트엔드 개발자 면접준비2"
description: ""
author: cotes
date: 2024-05-21 17:00:00 +0900
categories: [Interview]
tags: [취업, 면접]
pin: true
---

### 1. **HTML5에서 data- 속성의 사용 목적은 무엇인가요? 언제 사용해야 할까요?**

**답변:** `data-` 속성은 HTML 요소에 사용자 정의 데이터를 저장할 때 사용됩니다. 이를 통해 CSS나 JavaScript에서 추가 정보를 필요로 할 때 활용할 수 있습니다. 예를 들어, 버튼 클릭 시 특정 값을 참조하고 싶을 때 `data-` 속성에 저장된 데이터를 가져올 수 있습니다. 이 속성은 사용자에게 노출되지 않지만, JavaScript의 `dataset` API를 통해 쉽게 접근할 수 있습니다.

### 2. **this 키워드는 자바스크립트에서 어떻게 동작하나요? this의 문맥이 달라질 수 있는 상황에 대해 설명해 주세요.**

**답변:** `this`는 함수 호출 방식에 따라 다른 객체를 참조합니다. 일반 함수 호출에서는 전역 객체(`window` 또는 `global`)를 참조하고, 객체 메서드 내에서 호출될 경우 해당 객체를 참조합니다. 화살표 함수에서는 `this`가 선언 시점의 상위 스코프를 가리킵니다.

### 3. **React의 상태(state)와 속성(props)의 차이는 무엇인가요? 각각의 용도를 설명해 주세요.**

**답변:**

- **상태(state)**: 컴포넌트 내부에서 관리되는 데이터로, 동적인 데이터를 저장합니다. 상태가 변경되면 React는 해당 컴포넌트를 다시 렌더링합니다.
- **속성(props)**: 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 데 사용되는 읽기 전용 값입니다. `props`는 변하지 않으며, 자식 컴포넌트는 `props`를 통해 데이터를 받아와 렌더링합니다.

### 4. **SPA(Single Page Application)에서 성능 최적화를 위해 고려해야 할 사항은 어떤 것이 있나요?**



**답변:** SPA에서 성능 최적화를 위해 다음을 고려할 수 있습니다:

- **코드 스플리팅**: 초기 로드 시간을 줄이기 위해 필요한 페이지만 로드합니다.
- **Lazy Loading**: 이미지를 비롯한 리소스를 필요할 때만 로드합니다.
- **메모이제이션 기법**: React의 `memo`, `useMemo`, `useCallback`을 사용해 불필요한 재렌더링을 방지합니다.

### 5. **Next.js의 서버 사이드 렌더링(SSR)과 정적 사이트 생성(SSG)의 차이점은 무엇인가요?**

**답변:**

- **서버 사이드 렌더링(SSR)**: 요청 시 서버에서 페이지를 렌더링하여 클라이언트에 HTML을 전송합니다. 페이지 로드 시점에서 항상 최신 데이터를 제공할 수 있어 동적 콘텐츠에 적합합니다.
- **정적 사이트 생성(SSG)**: 빌드 시점에 페이지를 미리 렌더링하여 정적 HTML 파일을 생성합니다. 페이지 로딩 속도가 빠르고, CDN을 통해 배포할 수 있어 성능이 좋지만, 데이터가 자주 변경되지 않는 경우에 적합합니다.

### 6. **Next.js에서 getServerSideProps와 getStaticProps의 사용 사례는 무엇인가요?**

**답변:**

- **getServerSideProps**: SSR을 위해 페이지가 요청될 때마다 실행되며, 사용자 맞춤형 데이터나 최신 데이터를 가져오는 데 적합합니다.
- **getStaticProps**: SSG을 위해 빌드 시점에 한 번 실행되어 정적 HTML을 생성합니다. 데이터가 자주 변하지 않는 경우에 유용하며, 페이지가 빠르게 로드됩니다.

### 7. **Next.js의 API Routes 기능을 어떻게 활용하셨나요?**

**답변:** API Routes를 활용하여 백엔드 API를 서버리스 함수 형태로 구현할 수 있었습니다. 이를 통해 클라이언트에서 API를 호출하면 Next.js 서버가 직접 요청을 처리하고 필요한 데이터를 반환합니다. 이 기능을 사용해 사용자 인증, 데이터 처리 등의 백엔드 작업을 간편하게 구현할 수 있었습니다.

### 8. **Next.js에서 동적 라우팅을 어떻게 구현하나요?**

**답변:** 동적 라우팅은 파일 시스템 기반 라우팅을 사용하여 구현합니다. `[param].js` 형태로 파일을 생성하면, URL의 동적 경로를 자동으로 처리할 수 있습니다. 예를 들어, `[id].js` 파일을 생성하면 `/posts/123`와 같은 경로에서 `123`을 파라미터로 받아서 사용할 수 있습니다.

### 9. **Next.js에서 이미지 최적화는 어떻게 이루어지나요?**

**답변:** Next.js는 `next/image` 컴포넌트를 제공하여 이미지 최적화를 자동으로 처리합니다. 이 컴포넌트는 이미지의 크기 조정, 포맷 변환, 레이지 로딩을 지원하며, 웹 성능을 향상시킬 수 있습니다. 개발자는 단순히 `src`와 `alt` 속성을 설정하면 되고, 나머지는 Next.js가 최적화해줍니다.

### 포트폴리오 사이트 관련 질문

**Hash 기반 스크롤 관리에서 커스텀 훅을 구현했다고 하셨는데, 해당 훅의 핵심 기능과 이를 구현하는 데 어려움이 있었나요?**

**답변:** 핵심 기능은 URL의 해시값을 기반으로 각 섹션에 부드럽게 스크롤하는 것이었습니다. `Observer API`를 통해 섹션의 위치를 계산하고, 스크롤 시 실시간으로 해시값을 업데이트했습니다. 어려움은 Next.js에서 해시값을 바로 인식하지 못하는 부분이었고, 이를 커스텀 훅으로 해결했습니다.

**질문:** "Observer API 외에 다른 스크롤 관리 방법을 사용해본 적 있나요?"

**답변:** "Intersection Observer API도 사용해봤습니다. 특정 요소가 뷰포트에 들어올 때 이벤트를 트리거해, 스크롤 위치를 더 세밀하게 제어할 수 있었습니다."

### 팀 프로젝트 관련 질문

**JWT와 OAuth2를 사용하여 로그인 처리를 구현하셨는데, 두 인증 방식의 차이를 설명하고 프로젝트에 어떻게 적용했나요?**

**답변:** JWT는 토큰 기반 인증 방식으로, 사용자 정보가 토큰에 포함되어 있어 서버 요청 시 지속적인 세션 유지가 필요하지 않습니다. 반면 OAuth2는 외부 서비스(Google, Kakao 등)를 통한 인증 방식으로, 사용자가 추가 인증 없이 손쉽게 로그인할 수 있습니다. 프로젝트에서는 JWT를 기본 인증으로 사용하고, OAuth2는 SNS 로그인을 위해 적용했습니다.

**질문:** "JWT의 토큰 만료 시간 설정은 어떻게 했나요?"

**답변:** "Access Token의 만료 시간은 보안성 때문에 짧게 설정했고, Refresh Token은 상대적으로 길게 설정해 사용자가 로그아웃하지 않고도 세션을 연장할 수 있도록 했습니다."

### 감정 일기 프로젝트 관련 질문

**Chart.js를 활용해 감정을 시각화했다고 했는데, 데이터 시각화를 위해 어떤 차트 유형을 선택했고, 이유는 무엇인가요?**

**답변:** 라인 차트와 바 차트를 사용했습니다. 라인 차트는 감정 변화 추이를 시각적으로 잘 보여줄 수 있고, 바 차트는 각 감정의 빈도를 한눈에 비교할 수 있어 데이터 분석에 적합하다고 판단했습니다.

### Chat GPT 코딩 학습 서비스 관련 질문

**OpenAPI를 활용하여 코드 리뷰 및 피드백 기능을 구현했다고 하셨는데, API를 어떻게 통합했고, 사용자가 얻을 수 있는 가장 큰 이점은 무엇인가요?**

**답변:** OpenAPI를 통해 ChatGPT의 기능을 코드 리뷰 시스템에 통합했습니다. 사용자가 작성한 코드를 API로 전달하면 AI가 코드 스타일, 오류, 최적화 여부 등을 분석하고 피드백을 제공합니다. 이 기능 덕분에 사용자는 자동으로 개선된 코드를 빠르게 받을 수 있어 개발 속도가 향상됩니다.

### Clone 코딩 프로젝트 관련 질문

**React와 Vue 사이트를 클론 코딩하며 두 프레임워크의 가장 큰 차이점은 무엇이라고 생각하시나요?**

**답변:** React는 자유도가 높고 상태 관리를 유연하게 할 수 있어 큰 프로젝트에서 유리합니다. 반면 Vue는 상대적으로 더 간단한 구조와 명확한 규칙을 제공하여 빠른 프로토타입 제작에 적합하다고 느꼈습니다.

**질문:** "Vue의 컴포넌트 시스템을 어떻게 활용했나요?"

**답변:** Vue의 단일 파일 컴포넌트(SFC)를 활용해 HTML, CSS, JavaScript를 한 파일에 통합했습니다. 이를 통해 모듈화된 구조로 UI를 효율적으로 개발할 수 있었습니다.




