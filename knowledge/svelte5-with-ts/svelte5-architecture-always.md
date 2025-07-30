---
description: Svelte 5 아키텍처 및 컴포넌트 작성 규칙
globs: **/*.svelte,src/**/*.ts
---

# Svelte 5 아키텍처 규칙

## 🏗️ 기본 아키텍처
- **프레임워크**: Svelte 5 + TypeScript
- **라우팅**: SvelteKit 파일 기반 라우팅
- **상태관리**: Svelte context + reactive stores
- **스타일링**: 디자인 서버 CSS 클래스 우선 사용

## 📁 선호 파일 구조
```
src/
├── routes/           # 라우트 파일들
├── lib/
│   ├── components/   # 재사용 컴포넌트
│   ├── biz/         # 비즈니스 로직
│   └── api/         # API 클라이언트
```

## 🚫 지양사항
- **깊은 props 전달** - 컴포넌트 계층을 단순하게
- **불필요한 상태 중복** - 상태는 최소화하고 한 곳에서 관리
- **클래스 기반 컴포넌트** - 함수형 컴포넌트 사용

## 📝 컴포넌트 작성 원칙
- **최소 단위로 분리** - 재사용성 극대화
- **이벤트는 dispatch 대신 props로 메서드 전달** - 디버깅 편의성
- **Props는 단순하게 유지**
- **`@component` 태그로 문서화**
- **`$state`, `$derived` rune 적극 활용**

## 🎨 스타일링 방식
- **기본적으로 `<style>` 태그 사용 금지**
- **디자인 서버 CSS 클래스 활용**: `btn`, `input_txt`, `tbl_basic` 등
- **조건부 스타일링**: `class:` 지시어 사용
