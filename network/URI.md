# Uniform Resource Identifier (URI)

- 리소스를 식별하는 통일된 방식
- 인터넷상의 자원을 고유하게 식별할 수 있는 문자열
- URI로 문서, 이미지, 서비스 등 모든 종류의 리소스를 식별할 수 있다
- 다른 항목과 구분하는 데 필요한 정보를 포함한다

---

## URI 구조

URI 다이어그램 안에 **URL**과 **URN**이 포함됨
```scss
URI
├── URL (위치 지정)
└── URN (이름 지정)
```

- **URL (Uniform Resource Locator)** : 리소스의 위치를 지정하는 URI
- **URN (Uniform Resource Name)** : 리소스의 이름을 지정하는 URI

> ⚠️ URN만으로 리소스를 찾는 방법이 보편화되지 않음 → **URI는 사실상 URL과 같은 의미로 사용됨**

---

## URL 전체 문법
```스키마://userInfo@호스트명:포트번호/path?query#fragment```
### 1. **스키마 (Schema, 프로토콜)**
- 자원에 접근하는 방식 (예: `http`, `https`, `ftp`)

### 2. **userInfo (사용자 정보)**
- 인증 정보 포함 가능 (`사용자이름:비밀번호@`)
- 거의 사용되지 않음

### 3. **호스트명 (Host)**
- 도메인명 (`example.com`) 또는 IP 주소 (`192.168.1.1`)

### 4. **포트 번호 (Port, 생략 가능)**
- HTTP 기본 포트: `80`
- HTTPS 기본 포트: `443`
- `https://example.com:8080`

### 5. **Path (리소스 경로)**
- 서버 내 특정 리소스 위치
- `https://example.com:8080/path/to/resource`

### 6. **Query (쿼리 파라미터)**
- `?`로 시작하고 `key=value` 형태로 전달
- 여러 개의 쿼리는 `&`로 구분 (`?id=123&name=hello`)
- 숫자도 문자열로 전달됨

### 7. **Fragment (프래그먼트)**
- HTML 문서 내의 특정부분을 가리키는 내부 북마크 역할 (`#section1`)
- 주로 긴 문서에서 특정 섹션으로 바로 이동할 때 사용
- 서버로 전송되지 않음