### self-closing tag
- 명시적으로 닫는 태그가 필요 없음
- 기본 HTML 요소인지 아닌지 명확한 차이를 가져야함
- 리액트 컴포넌트라면 하위에 HTML 관련된 아무것도 존재하지 않는다면 닫는 태그 없으면 깔끔

### fragment
- key가 필요한 경우 숏컷 사용 불가능
- 불필요한 경우 사용하지 말자
  - ex) 최종적으로 꼭 감싸는 경우, null 반환해도 되는데 <></> 사용하는 경우

### 컴포넌트 네이밍
- 일반적으로 컴포넌트는 PascalCase
- 기본 HTML 요소는 lower case
- router based file name (kebab-case)

### JSX 컴포넌트 함수로 반환
```typescript
return (
  <div>
    {TopRender()} //지양
    <TopRender /> //지향
  </div>
)
```
- 함수로 return 하는 경우
  - scope를 알아보기 어렵다
  - 반환 값을 바로 알기 어렵다
  - props 전달 등 일반적인 패턴이 아니다

### 컴포넌트 내부에 컴포넌트 선언
```typescript
function OuterComponent() {
  const InnerComponent = () => {
    return ();
  }
}
```
- 결합도가 증가
  - 구조적으로 스코프적으로 종속된 개발이 된다
  - 나중에 확장성이 생겨서 분리될 때 굉장히 힘들어진다
- 성능 저하
  - 상위 컴포넌트 리렌더 => 하위 컴포넌트 재생성
```typescript
const InnerComponent = () => {
  return ();
}

function OuterComponent() {
}
```
### displayName
- devtools에서 익명 함수를 쉽게 디버깅하려면 disPlayName 속성 사용

### 컴포넌트 구성
- 상수는 컴포넌트 외부로
- interface도 컴포넌트 외부로
- 컴포넌트를 어떻게 선언할 것인지 , props 구조 분해 할당 어떻게 할 건지 -> 개인 취향
- 플래그성 상태, ref, third-party 라이브러리를 위에
- 커스텀 훅
- useState - 컴포넌트 내부 상태
- 이벤트 핸들러 (리액트와 관계 없는건 외부로)
- useEffect -> main JSX와 가장 가까운 곳에 위치
- JSX 반환
- styled-component 하단 위치 (개인 선호)
- 정답은 없다!
