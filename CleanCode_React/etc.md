#### import React from 'React'
- React 17부터 제거 가능
- jsx-runtime 자동 삽입 
```javascript
//jsx
function App() {
  return <h1>Hello World</h1>;
}

//내부적으로 React.createElement 함수 호출로 변환
function App() {
  return React.createElement('h1', null, 'Hello World');
}
```
```javascript
// 자동으로 추가됨
import { jsx as _jsx } from 'react/jsx-runtime';

function App() {
  return _jsx('h1', { children: 'Hello World' });
}
```
- `React.useEffect` 처럼 명시적으로 사용해야할 경우는 예외<br><br>

#### 리액트 폴더 구조
- 시작부터 거창하게 가져갈 필요 없음
- depth를 쓸데 없이 늘리지 말 것 
- 결합도가 높으면 prefix를 활용하는 것도 방법<br><br>

####  window.location.reload()
- SPA 입장에서 `window.location.reload()`는 앱을 완전히 껐다 켜는 수준이다
- state 다 날라갈수도 있음 -> `window.location.reload()`를 꼭 사용해야 하는 경우 local storage 사용
- 전체 앱을 리로드하지 않고 필요한 컴포넌트만 리렌더링하도록 <br><br>

####  Primitive UI
- 도메인을 넣기보다는 UI를 묘사한다
- 최대한 시맨틱하게 구현하려고 노력해보자
```javascript
// Bad Case
<TodoList />
<TodoItem />

// Good Case
<FeedList />
<CardList />
```