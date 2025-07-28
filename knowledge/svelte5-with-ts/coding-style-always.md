---
description: 코딩 스타일 규칙 - 네이밍, 포맷팅, ESLint 준수
globs: **/*.{ts,js,tsx,jsx,svelte}
alwaysApply: true
---
# 📝 Svelte 5 + TS 코드 스타일 지침
---

## 🏷 파일 이름 & 컴포넌트

- `.svelte` 파일은 **kebab-case** 사용 (예: `user-profile.svelte`)
- 컴포넌트 import 시 **PascalCase** 사용 (예: `import UserProfile from './user-profile.svelte'`)

---

## 📝 네이밍 컨벤션
- **변수/함수**: camelCase (예: `userName`, `handleClick`)
- **클래스/인터페이스**: PascalCase (예: `UserInfo`, `ApiResponse`)
- **상수**: UPPER_SNAKE_CASE (예: `MAX_LENGTH`)
- **파일명**: PascalCase.svelte (예: `UserProfile.svelte`)

## 🎨 포맷팅
- **들여쓰기**: 2칸 스페이스
- **따옴표**: 큰따옴표 (`"`) 사용
- **세미콜론**: 필수 사용
- **trailing commas**: 사용하지 않음
- **최대 줄 길이**: 제한 없음

## 🔧 ESLint 설정
### 비활성화된 규칙:
- `no-plusplus`
- `no-console` 
- `no-underscore-dangle`
- `no-param-reassign`

### 경고 규칙:
- `no-unused-vars`
- `no-trailing-spaces`
- `import/order`
- `prefer-template`

## 💡 코드 품질
- **중복 코드 최소화** - 공통 로직 추출
- **중첩 if문 지양** - early return 패턴 사용
- **유효성 검사는 유틸 메서드로 분리**
- **인라인 주석은 한글로 작성**
- **JSDoc/Javadoc 스타일 문서화 주석 사용**


## 🧰 *.svelte 파일 정의 공통 구조

- **Import Section**
  - 외부 → 공통 → 모듈 외부 컴포넌트 모듈 내부 컴포넌트 순
- **Props Section**
  - interface Props + $props()
- **Type Section**
  - 파일 내 type, interface, enum 정의
- **Const Section**
  - 상수 정의(변수값 초기화 이후 변동 없는 변수)
  - 대문자 SNAKE_CASE 정의
- **Svelte Section**
  - svelte 라이브러리를 이용한 변수 정의
  - ex) import { X } from 'svelte';
- **Bind Section**
  - HTML 요소 바인딩(bind:this)
  - Svelte 컴포넌트 바인딩(bind:this)
- **Variable Section**
  - 일반 변수
- **Reactivity Section**
  - `$derived` 파생 상태
  - Store Subscribe 메서드
- **Method Section**
  - 일반 메서드
- **Event Handler Section**
  - DOM 또는 컴포넌트 이벤트 메서드 정의
- **Lifecycle Hook Section**
  - `onMount`, `onDestroy`

## 🎯 완전한 컴포넌트 템플릿 (스니펫 기준)

```svelte
<!--
  @component
  컴포넌트 설명입니다. 컴포넌트가 아닌 경우 삭제해 주세요
-->
<script lang="ts">
  // Import Section
  import type { Snippet } from 'svelte';
  import { onMount } from 'svelte';
  import { I18n } from '$lib/common/i18n';

  // Props Section
  interface Props {
    title?: string;
    isVisible?: boolean;
    onClick?: () => void;
    children?: Snippet;
  }

  let {
    title = '',
    isVisible = false,
    onClick = () => {},
    children
  }: Props = $props();

  // Type Section
  interface User {
    name: string;
    email: string;
  }

  // Const Section
  const DEFAULT_CONFIG = {
    timeout: 5000
  };

  // Svelte Section
  let count = $state(0);
  let user = $state<User>({ name: '', email: '' });

  // Bind Section
  let inputElement: HTMLInputElement;
  let modalElement: HTMLDialogElement;

  // Variable Section
  let isLoading = false;

  // Reactivity Section
  let doubled = $derived(count * 2);
  let isEven = $derived(count % 2 === 0);

  // Method Section
  const processData = (): void => {
    // 처리 로직
  };

  // Event Handler Section
  const handleSubmit = (event: Event): void => {
    event.preventDefault();
    onClick();
  };

  // Lifecycle Hook Section
  onMount(() => {
    console.log('컴포넌트가 마운트되었습니다');
  });
</script>

<!-- 여기서부터 마크업 -->
<div>
  <h1>{title}</h1>
  {#if isVisible}
    <button onclick={handleSubmit}>클릭</button>
  {/if}
  {@render children?.()}
</div>

<style>
  div {
    padding: 1rem;
  }
</style>
```

---

## 📝 Snippet 렌더링 패턴

```svelte
<!-- ✅ 기본 children 렌더링 -->
{@render children?.()}

<!-- ✅ 조건부 렌더링 -->
{#if children}
  {@render children()}
{/if}

<!-- ✅ 매개변수와 함께 렌더링 -->
{@render children?.(user, handleClick)}
```

---

## 🧹 ESLint & 코드 품질 규칙
- **비활성화 허용**: no-console, no-plusplus
- **경고 수준 대응**: no-unused-vars, prefer-template, import/order 등 자동 리팩토링
- **패턴**:
	- 중첩 if → early return
	- 유효성 검사 → utils로 분리
	- 반복 로직 → helper 함수
- **주석**:
	- 함수/파일: JSDoc
	- 인라인: 한글로 설명

---

## ⚠️ 주의사항
- **createEventDispatcher 사용 금지** - 콜백 함수 사용
- **$effect는 사이드 이펙트 필요 시에만** 사용
- **타입을 명시적으로 정의**
- **Props는 interface 분리 방식 우선 사용**



