## Tuple
- 정해진 길이와 각 위치마다 특정 타입을 가진 배열
- 타입스크립트에만 있는 문법
- 잘 쓰진 않지만 사용하면 유용한 상황이 있음
```typescript
const color : [number, number, number] = [0,0,0];
```
```typescript
type HTTPResponse = [number, string];
const goodRes: HTTPResponse = [200, "OK"]
```

### 한계
- 배열 메서드를 사용할 때 주의해야 한다
  - push 메서드는 타입 검사를 우회할 수 있음
```typescript
// [number, string] 타입의 tuple 선언
const userInfo: [number, string] = [1, "Sam"];

// 원래 tuple은 두 개의 요소만 가져야 하지만
// push 메서드를 사용하면 타입 체크를 우회할 수 있음
userInfo.push(true); // 컴파일러는 이를 허용함!

console.log(userInfo); // 출력: [1, "Sam", true]

// 그러나 타입 시스템에서는 여전히 [number, string] 타입으로 인식
// 세 번째 요소에 접근하려고 하면 타입 오류 발생
const thirdElement: boolean = userInfo[2]; // 타입 에러: 'userInfo'의 인덱스 '2'에 요소가 없습니다.
```
<br><br>

## Enum
- 코드 전체에서 재사용할 수 있는 명명된 상수의 집합
- Enum의 기본값은 0부터 시작
- 타입스크립트에만 있는 문법
```typescript
enum OrderStatus {
    PENDING,
    SHIPPED,
    DELIVERED,
    RETURNED
}
const status = OrderStatus.SHIPPED;
```
- 명시적으로 값 지정 가능
```typescript
enum Direction {
  UP = "UP",
  DOWN = "DOWN",
  LEFT = "LEFT",
  RIGHT = "RIGHT"
}
```

### 한계
- Enum은 JavaScript 런타임에서 객체로 변환되어 번들 크기를 증키시킨다.
  - 일부 번들러에서 tree-shaking이 되지 않아 불필요한 코드의 용량이 증가
  >💡 tree-shaking: 번들리 과정에서 사용되지 않는 코드를 제거해 최종 번들 크기를 줄여는 방식
- 보통 enum보다 union 타입 사용을 선호 