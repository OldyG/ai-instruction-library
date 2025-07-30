---
description: 
globs: *.svelte,*.ts
---






---

## 🔄 Reactivity – Svelte 5 룬 사용

- 상태 초기화: `let count = $state(0)`
- 파생 상태: `let doubled = $derived(count * 2)`
- 부수 효과: `$effect(() => {...})`

**⚠ BEFORE/AFTER 예시**

```svelte
// ❌ BEFORE (Svelte 4)
<script lang="ts">
  let count = 0;
  $: doubled = count * 2;
</script>

// ✅ AFTER (Svelte 5)
<script lang="ts">
  let count = $state(0);
  let doubled = $derived(count * 2);
  $effect(() => console.log(count));
</script>
```

---

## 📊 Props 시스템 (Svelte 5) - 권장 방식

```typescript
// ✅ 권장: interface 분리 방식 (스니펫 기준)
// Import Section
import type { Snippet } from 'svelte';
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
```

```typescript
// ⚠️ 대안: 인라인 타입 방식 (복잡한 타입용)
let {
  /** 사용자 정보 */
  user,
  /** 로딩 상태 */
  isLoading = false,
  /** 저장 콜백 */
  onSave
}: {
  user: User;
  isLoading?: boolean;
  onSave: (user: User) => void;
} = $props();
```

---

## 🧩 네이밍 & 변수 규칙
- **변수/함수**: `camelCase`
- **컴포넌트 이름**: `PascalCase`
- **상수**: `UPPER_SNAKE_CASE`
- **이벤트 핸들러**: `handle` + 카멜케이스 (예: `handleSubmit`)
- **콜백 Props**: `on` + 파스칼케이스 (예: `onClick`, `onSave`)
- **바인딩 변수**: `Element` 접미사 (예: `inputElement`, `modalElement`)

---

## 🎨 포맷팅 룰
- 들여쓰기: **2칸 공백**
- 문자열: **큰따옴표 (")**
- 세미콜론: **항상 사용**
- trailing comma: **금지**
- 줄 길이: **최대 120자**
- 태그 닫기: **self-closing** (`<br />`)
- import 정렬: **external → internal → 상대경로**

---

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

---

