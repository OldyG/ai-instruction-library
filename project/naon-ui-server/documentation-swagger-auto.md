---
description: 문서화 및 Swagger 사용 규칙
globs: src/lib/api/**/*.ts,**/*.md,docs/**/*
alwaysApply: false
---

# 문서화 및 Swagger 규칙

## 📚 문서화 표준
- **Swagger 사용** - API 문서화는 Swagger로 표준화
- **JSDoc/Javadoc 스타일** - 모든 함수/메서드에 문서화 주석 필수

## 💻 주석 포맷 가이드

### TypeScript/JavaScript:
```typescript
/**
 * 사용자 정보를 저장합니다.
 * @param userData 저장할 사용자 데이터
 * @param options 저장 옵션
 * @returns 저장 결과를 담은 Promise
 * @throws {ValidationError} 데이터 검증 실패 시
 */
const saveUser = async (userData: UserData, options: SaveOptions): Promise<SaveResult> => {
  // 구현 내용
};
```

### Java (참고용):
```java
/**
 * 사용자 정보를 조회합니다.
 * @param userId 사용자 ID
 * @return 사용자 정보
 * @throws UserNotFoundException 사용자를 찾을 수 없는 경우
 */
public UserInfo getUserInfo(String userId) throws UserNotFoundException {
    // 구현 내용
}
```

### Svelte 컴포넌트:
```svelte
<!--
  @component
  사용자 목록을 표시하고 관리하는 컴포넌트입니다.
  
  ## 기능
  - 사용자 검색 및 필터링
  - 페이지네이션 지원
  - 사용자 선택 및 편집
  
  ## 사용법
  ```svelte
  <UserList 
    users={userList} 
    onUserSelect={(user) => handleUserSelect(user)}
  />
  ```
-->
```

## 📋 필수 문서화 항목
- **함수/메서드 목적** - 무엇을 하는지
- **매개변수** - 각 파라미터의 의미와 타입
- **반환값** - 반환되는 데이터의 의미와 타입
- **예외사항** - 발생 가능한 에러 상황
- **사용 예시** - 복잡한 경우 사용법 포함

## 🌐 다국어 주석
- **인라인 주석**: 한국어 사용
- **문서화 주석**: 영어 또는 한국어 (프로젝트 정책에 따라)
- **변수명/함수명**: 영어 (camelCase/PascalCase)

## 📊 Swagger 문서화
- **API 엔드포인트** 모두 문서화
- **Request/Response DTO** 명확히 정의
- **에러 코드 및 메시지** 포함
- **인증/권한** 요구사항 명시
