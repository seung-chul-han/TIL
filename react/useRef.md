# useRef().current 가 null이 되는 현상


```jsx
const testRef = useRef(null);


return (
  <div ref={testRef} />
);

```

일때 useRef는 useEffect, useState처럼 값이 변경되면 새로 렌더링 하지 않는다.
(읽기 전용이라 업데이트 되지 않는다)
그리고 react-query나 swr같은 것을 쓰게 되면 캐시된 데이터를 읽어 오므로 새로 렌더링 되지 않는다.

## 해결 방법
ref를 같는 요소를 컴포넌트로 만들어 주었고, 데이터도 같이 넘겨줘서 무조걸 리렌더링이 되도록 하였다
