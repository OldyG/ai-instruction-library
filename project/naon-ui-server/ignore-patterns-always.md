---
description: 작업 시 무시해야 할 파일 및 디렉토리 패턴
globs: **/*
alwaysApply: true
---

# 무시할 파일/디렉토리 패턴

## 🚫 절대 수정/참조하지 말 것
다음 패턴의 파일들은 작업 대상에서 제외하고 참조하지 마세요:

### 일반적인 제외 패턴:
- `node_modules/` - NPM 패키지 디렉토리
- `.git/` - Git 버전 관리 디렉토리
- `dist/` - 빌드 산출물 디렉토리
- `build/` - 빌드 산출물 디렉토리
- `.husky/` - Git hooks 관리 디렉토리

### 개발 도구 관련:
- `.vscode/` - VS Code 설정 디렉토리
- `ai-instructions/` - AI 지침 디렉토리 (읽기만 가능)

### 임시/테스트 파일:
- `1.txt` - 임시 파일
- `2.txt` - 임시 파일  
- `rebel.xml` - 개발 도구 설정 파일

## 📖 읽기 전용 파일
다음 파일들은 참조만 가능하고 수정하지 마세요:

### AI 지침 파일들:
- `ai-instructions/**/*.md` - AI 작업 지침 (참조용)
- `.cursor-instructions.md` - 레거시 지침 파일
- `.cursorrules` - 레거시 규칙 파일 (새 .cursor 시스템으로 대체됨)

### 설정 파일들:
- `package.json` - 패키지 설정 (의존성 추가 시에만 수정)
- `eslint.config.js` - ESLint 설정
- `tsconfig.json` - TypeScript 설정

## ✅ 작업 가능 영역
다음 영역에서만 파일 생성/수정이 허용됩니다:

### 소스 코드:
- `/packages/naon-webapp/src/**` - 모든 소스 코드
- `/packages/naon-webapp/static/resources/i18n/**` - 다국어 리소스

### 문서:
- `README.md` - 프로젝트 문서 (필요시)
- `/docs/**` - 프로젝트 문서화 (필요시)

## 🔍 참조 시 주의사항
- **임시 파일 생성 시** 반드시 작업 완료 후 삭제
- **테스트 파일 생성 시** `.gitignore`에 등록된 경로 사용
- **설정 파일 수정 필요 시** 사용자에게 명시적 확인 후 진행
