---
description: API 개발 및 클라이언트 작성 규칙
globs: src/lib/api/**/*.ts,src/lib/biz/**/*.ts
alwaysApply: false
---

# API 개발 규칙

## 🏗️ API 클라이언트 구조
- **ApiClient 클래스 상속** - 모든 API 클라이언트는 ApiClient를 상속
- **DTO 분리** - Request/Response DTO를 명확히 분리
- **Result<T> 래핑** - 모든 API 응답은 Result<T> 타입으로 래핑
- **CustomException 사용** - 에러 처리는 CustomException 활용

## 📝 DTO 네이밍 규칙
```typescript
// Request DTO
export interface SaveUserRequest {
  name: string;
  email: string;
}

// Response DTO  
export interface SaveUserResponse {
  userId: string;
  success: boolean;
}
```

## 🔧 API 클라이언트 예시
```typescript
export class UserApiClient extends ApiClient {
  /**
   * 사용자를 저장합니다.
   * @param request 사용자 저장 요청
   * @returns 저장 결과
   */
  async saveUser(request: SaveUserRequest): Promise<Result<SaveUserResponse>> {
    try {
      const response = await this.post<SaveUserResponse>('/api/user', request);
      return Result.success(response);
    } catch (error) {
      return Result.failure(new CustomException('사용자 저장 실패', error));
    }
  }
}
```

## 📚 문서화
- **Swagger 사용** - API 문서화는 Swagger 활용
- **JSDoc 필수** - 모든 메서드에 JSDoc 주석 작성
- **타입 안전성** - TypeScript strict mode 활용

## 🚨 에러 처리
- **빠른 실패** - 에러 발생 시 즉시 반환
- **구체적인 에러 타입** - 일반적인 Exception 대신 구체적 에러 사용
- **로깅 포함** - 에러 발생 시 적절한 컨텍스트와 함께 로깅
