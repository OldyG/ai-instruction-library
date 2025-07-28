---
description: Svelte 5 컴포넌트 작업 시 상세 컨벤션 규칙
globs: **/*.svelte
alwaysApply: false
---

# Svelte 5 컴포넌트 상세 컨벤션

## 📋 섹션 순서 (반드시 준수)
- [svelte.code-snippets](mdc:.vscode/svelte.code-snippets) 참조
  - 개발자는 해당 기능을 사용하여 신규 파일 만들고 init 또는 init-2를 이용하여 컴포넌트 기본구성함
  - [스벨트_정의_샘플.svelte](mdc:.cursor/스벨트_정의_샘플.svelte) 는 init-2 명령을 이용한 결과물 파일


2. **import Section**
3. **Props Section** 
4. **Type Section**
5. **Const Section**
6. **Svelte Section** (`$state`, `$derived`)
7. **Bind Section** (HTML 요소 바인딩)
8. **Variable Section** (일반 변수)
9. **Reactivity Section** (`$derived` 파생 상태)
10. **Method Section** (일반 메서드)
11. **Event Handler Section** (DOM 이벤트)
12. **Lifecycle Hook Section** (`onMount`, `onDestroy`)

## 🏷️ 네이밍 규칙
- **이벤트 핸들러**: `handle` 접두사 + 카멜케이스 (예: `handleSubmit`)
- **콜백 Props**: `on` 접두사 + 파스칼케이스 (예: `onSave`, `onUserSelect`)
- **바인딩 변수**: `Element` 접미사 (예: `inputElement`, `modalElement`)

## 🔧 함수 정의
```typescript
// ✅ 올바른 방식: const + 화살표 함수
const handleClick = (event: Event): void => {
  // 처리 로직
};

// ❌ 잘못된 방식: function 키워드
function handleClick(event: Event): void {
  // 처리 로직
}
```

## 📊 Props 시스템 (Svelte 5)
```typescript
interface Props {
  onClick?: () => void;
  children?: Snippet;
}

let { onClick = () => {}, children }: Props = $props();
```


## 📝 문서화
```svelte
<!--
  @component
  사용자 프로필을 표시하고 편집할 수 있는 컴포넌트입니다.
  
  ## 기능
  - 실시간 유효성 검사
  - 자동 저장 기능
-->
```

## ⚠️ 주의사항
- **svlete 4문법 사용 금지**
  - svelte 4와 5는 문법적으로 많은 차이가 생겼습니다. 
  - AI가 알고 있는 정보가 4버전이라면 반드시 5버전을 숙지 후 작업하세요
- **createEventDispatcher 사용 금지** - 콜백 함수 사용
- **$effect는 사이드 이펙트 필요 시에만** 사용
- **타입을 명시적으로 정의**
