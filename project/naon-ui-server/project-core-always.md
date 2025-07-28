---
description: 프로젝트의 핵심 디렉토리 구조 및 경로 규칙을 항상 적용함. Fix this, Refactor this 명령 시 강제됨.
globs: **/*
alwaysApply: true
---

# 📁 프로젝트 핵심 구조 규칙

## ✅ 필수 디렉토리 구조
- `/src/pages`: 페이지 컴포넌트
- `/src/components`: 공통 UI 컴포넌트
- `/src/stores`: Svelte store 모듈
- `/src/lib`: 유틸 및 헬퍼 함수
- `/src/routes`: 라우팅 처리용

## 📄 파일 구조 패턴
- 페이지: `/pages/login.svelte`, `/pages/home.svelte`
- 라우터 연결 시 반드시 페이지 디렉토리 구조를 따름
- store는 반드시 `camelCase.ts` 네이밍 사용

## 🧠 행동 지침
- 구조가 어긋난 경우 자동 수정 제안
- 존재하지 않는 필수 디렉토리가 발견되면 생성하도록 유도
- 잘못된 위치의 파일이 발견되면 적절한 위치로 이동 제안
