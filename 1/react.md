# React

{% hint style="info" %}
**필독**

* [**React 공식문서**](https://ko.reactjs.org/)**,** [**React Beta 문서**](https://beta.reactjs.org/) (권장)
* [**React 코어 개발자가 쓴 React에 대한 이해를 돕는 글**](https://overreacted.io/ko/react-as-a-ui-runtime/)
{% endhint %}

사용자 인터페이스를 만들기 위한 JavaScript 라이브러리

React는 컴포넌트를 중심으로 동작한다.&#x20;



### 렌더링

* **createRoot**

```typescript
// main.tsx

import { createRoot } from "react-dom/client";
import App from "./App";

function main() {
  const element = document.getElementById("root");

  if (!element) {
    return;
  }

  const root = createRoot(element);

  root.render(<App />);
}

main();

```

```html
// index.html

<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Demo App</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="./src/main.tsx"></script>
  </body>
</html>

```

React는 변경된 부분만 업데이트 한다.

* Reconciliation(재조정)
* diffing algorithm



### 리렌더링

React는 **컴포넌트의 상태**가 변경될 때마다 렌더링을 예약합니다.

**상태**를 변경한다는 것은 `setState` 함수(React hooks에서는 `useState`)를 실행할 때, React 트리거가 업데이트된다는 것을 의미합니다. 이는 컴포넌트의 render 함수가 호출된다는 것을 의미할 뿐만 아니라, **props 변경 여부와 관계없이 모든 하위 컴포넌트들이 리렌더링 된다는 것을 의미합니다.**

* [React는 컴포넌트를 언제 다시 리렌더링 할까요?](https://velog.io/@surim014/react-rerender)
* [왜 리액트에서 리렌더링이 발생하는가.](https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-%EC%99%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94%EA%B0%80-74dd239b0063)
* [React 렌더링 동작에 대한 (거의) 완벽한 가이드](https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior)

