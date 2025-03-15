## useContext
- React의 Context API를 사용하여 전역 상태를 쉽게 관리할 수 있도록 함
- context를 사용하면 컴포넌트를 재사용하기 어려워 질 수 있기때문에 꼭 필요할 때만 사용한다
- props drilling을 피하기 위한 목적이라면 컴포넌트 합성을 먼저 고려해보자
- 사용 예시: User, Theme, Language 

<br>

### 사용법
1. createContext
```typescript
export const ThemeContext = createContext(null); // 초기값을 null
```
- context를 생성한다


2. provider로 값 전달
```typescript
return (
	<ThemeContext.Provider value={{isDark, setIsDark}> 
		<Page />
	</ThemeContext.Provider>
);
``` 
- context를 사용할 컴포넌트의 상위에서 Provider로 감싸고, value를 성정해줘야 한다


3. useContext로 값 가져오기
```typescript
const data = useContext(ThemeContext);

console.log(data); //data에는 전달한 isDark와 setIsDark가 들어있음

const { isDark, setIsDark } = useContext(ThemeContext);
```


### zustand와의 비교
- useContext의 값이 변경되면 하위 컴포넌트가 모두 재랜더링
- zustand는 상태를 구독한 컴포넌트만 재렌더링