## DB 테이블 `NOT NULL` vs `DEFAULT`

### 개념
- `NOT NULL`: 해당 필드는 `NULL` 값을 저장할 수 없음 
- `DEFAULT` : 값이 명시되지 않은 경우 기본값을 자동으로 설정

### 문제 상황
특정 컬럼(DECIMAL(10,2))에 DEFAULT 0.00을 설정했지만, 여전히 NULL 값이 저장됨

### 원인
- `NULL`은 명시적으로 설정된 값
  - `INSERT` 시 `NULL`로 명시되면 기본값이 적용되지 않는다
- `DEFAULT` 값은 `INSERT`문에서 해당 컬럼이 생략될 때 적용
  - `NULL`을 명시적으로 입력하면 기본값이 적용되지 않고` NULL`이 그대로 저장됨

### 시도했던 방법들
- `@Column(nullable = false, columnDefinition = "DECIMAL(10,2) DEFAULT 0.00")`
    - DDL 생성시의 조건이라 INSERT(DML)에 적용되지 않는다
- `@DynamicInsert` 사용
  - JPA의 기본 전략: 엔티티의 모든 필드를 쿼리로 날린다
  - 해당 어노테이션을 사용하면 실제 등록되는 column만 쿼리로 날라간다
  - `INSERT` 시 값이 `NULL`인 컬럼이 포함되지 않는 것 → 따라서 `default` 값으로 들어간다
  - 일관성이 깨진다  (모든 `INSERT`에서 동일한 컬럼을 업데이트하지 않게 됨)

### 해결
- 해당 DTO에 초기값을 설정하여 NULL이 들어가지 않도록 변경