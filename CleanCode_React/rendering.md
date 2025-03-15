### 공백처리
```typescript
{' '}
```
- &ndsp 대신 jsx로 처리

### 0은 JSX에서 유효한 값
```typescript
export default Component = () => {
  return (
    {items.length && ...}
  );
}
```
- items.length가 0이면 아무것도 렌더링하지 않기를 기대하지만 0이 출력됨
- JSX에서 0은 유효한 값
```typescript
export default Component = () => {
  return (
    {items.length > 0 ? ... : ...}
  );
}
```
- 명확하게 조건을 명시해주는 게 좋다
### 리스트 내부에서의 키
- key를 부여하자
- list 만들 때 꼭! ID를 부여하자
- 혹은 새로운 아이템을 추가하는 함수를 만들 때 그 때 고유한 값을 넣어주자
- 순회 시 key를 넣을 때 단순 index를 넣거나 렌더링마다 항상 새로운 값을 넣는 것 지양
  -  `uuid`, `new Date().toString()`, `index` 지양
### 안전하게 Raw HTML 다루기
- XSS 공격의 위험성을 줄이기 위해 DOMPurify 라이브러리 사용
```typescript
import DOMPurify from 'dompurify';

const safeHTML = (html: string) => ({
__html: DOMPurify.sanitize(html),
});

const Component = ({ content }: { content: string }) => (
  <div dangerouslySetInnerHTML={safeHTML(content)} />
);
```