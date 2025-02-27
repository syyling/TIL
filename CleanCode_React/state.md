### 올바른 초기값 설정
```javascript
//bad
const [number, setNumber] = useState();

//good
const [number, setNumber] = useState(0);
```
- 초기값이 없는 상태는 undefined가 되어 예기치 않은 버그를 발생시킬 수도 있다.

### 업데이트되지 않는 값
업데이트되지 않는 값은 컴포넌트 외부로 빼는 것이 좋음
```javascript
// Bad
function Component() {
  const [constantValue] = useState('이 값은 변하지 않습니다');
  // ...
}

// Good
const CONSTANT_VALUE = '이 값은 변하지 않습니다';
function Component() {
  // ...
}
```
### 플래그 상태
`useState` 쓰지 않고 컴포넌트 내부의 변수로

### 불필요한 상태
- 불필요한 상태를 만들지 말고 컴포넌트 내부 변수 const로 상태를 선언하는게 좋은 경우도 있음.
- useState를 사용하면 리액트에 의해 관리되는 값이 늘어나는 것 -> 렌더링에 영향을 주는 값이 늘어나서 관리포인트가 늘어난다.
- props를 useState에 넣지 않고 바로 return문에 사용하기
- 
### useState 대신 useRef
- useRef는 가변 컨테이너 같은 것
- 리렌더링 방지가 필요하다면 useState 대신 useRef
- 컴포넌트의 전체적인 수명과 동일하게 지속된 정보를 일관적으로 제공해야하는 경우
- 트리거가 작동될 필요가 있는 경우
- useRef는 꼭 dom에 attach해서 쓸 필요 없음
```javascript
const isMount = useRef(false);

useEffect(() => {
  if (!isMount.current) {
    isMount.current = true;
    // 최초 마운트 시에만 실행
  }
}, []);
```


### 연관된 상태 단순화하기

### 연관된 상태 객체로 묶어내기

### useState에서 useReducer로 리팩토링

### 상태 로직 Custom Hooks로 뽑아내기

### 이전 상태 활용하기
