# NAON UI Server 프로젝트

## 프로젝트 개요
- **프로젝트명**: naon-ui-server
- **버전**: 1.0.0
- **Node.js 버전**: ^18 || ^20
- **프레임워크**: Svelte 5 + SvelteKit + TypeScript
- **아키텍처**: 모노레포 구조 (workspaces)

## 주요 특징
- 한국의 그룹웨어 솔루션 (전자우편, 메신저, 업무관리 등)
- 다국어 지원 (한국어, 영어, 일본어, 베트남어, 중국어)
- 모던 웹 기술 스택 (Svelte 5, TypeScript, Vite)
- 컴포넌트 기반 모듈러 아키텍처

## 프로젝트 구조

### 루트 디렉토리
```
naon-ui-server/
├── packages/
│   └── naon-webapp/          # 메인 웹 애플리케이션
├── config/base/              # 기본 설정 파일들
├── 테스트케이스 계획서/        # 테스트 문서들
├── .cursor/rules/           # 상세 규칙 파일들
└── .vscode/                 # VS Code 설정
```

### 메인 애플리케이션 구조 (packages/naon-webapp/)
```
src/
├── routes/                  # SvelteKit 라우트
│   ├── [[header]]/         # 헤더가 포함된 페이지들
│   │   ├── eml/           # 전자우편 모듈
│   │   ├── msgr/          # 메신저 모듈
│   │   ├── work/          # 업무관리 모듈
│   │   ├── res/           # 예약관리 모듈
│   │   └── ... (기타 모듈들)
│   ├── auth/              # 인증 관련
│   └── login/             # 로그인 페이지
├── lib/
│   ├── api/               # API 클라이언트들
│   │   ├── eml/          # 전자우편 API
│   │   ├── msgr/         # 메신저 API
│   │   └── ... (모듈별 API)
│   ├── biz/              # 비즈니스 로직 컴포넌트
│   ├── common/           # 공통 유틸리티
│   ├── store/            # 상태 관리
│   └── constants/        # 상수 정의
└── static/
    └── resources/
        ├── i18n/         # 다국어 리소스
        ├── images/       # 이미지 자원
        └── libs/         # 외부 라이브러리
```

## 주요 모듈

### 1. 전자우편 (EML)
- 메일 송수신, 메일함 관리
- 라벨 관리, 전송 설정
- API: `EmlUserApiClient`, `EmlMngApiClient`

### 2. 메신저 (MSGR)
- 실시간 채팅, 파일 공유
- WebSocket 통신
- API: `MsgrApiClient`, `MsgrWebSocketApiClient`

### 3. 업무관리 (WORK)
- 업무 생성, 진행 상태 관리
- 칸반 보드, 리포트
- API: `WorWorkApiClient`, `WorMngApiClient`

### 4. 예약관리 (RES)
- 회의실, 자원 예약
- 반복 일정 지원
- API: `ResApiClient`, `ResMyApiClient`

## 기술 스택

### 프론트엔드
- **Svelte 5**: 최신 반응형 프레임워크
- **TypeScript**: 타입 안전성
- **SvelteKit**: 풀스택 프레임워크
- **Vite**: 빌드 도구

### 주요 라이브러리
- **UI**: Bootstrap 5, SvelteStrap
- **차트**: Chart.js, C3.js
- **에디터**: Monaco Editor, CKEditor5
- **다국어**: svelte-i18n
- **날짜**: dayjs, date-fns
- **통신**: WebSocket, STOMP

## 개발 환경 설정

### 스크립트 명령어
```bash
# 개발 서버 실행
npm run local:webapp      # 로컬 개발 모드
npm run dev:webapp        # 개발 모드

# 빌드
npm run build             # 프로덕션 빌드

# 코드 품질
npm run lint              # ESLint 검사
npm run format            # Prettier 포맷팅
npm run check             # Svelte 타입 체크

# 테스트
npm run test              # Playwright 테스트
```

### 환경별 실행
- **개발**: `cross-os dev -mode development`
- **로컬**: `cross-os dev -mode localpc`
- **프로덕션**: `cross-os dev -mode production`

## 코딩 컨벤션

### 네이밍 규칙
- **변수/함수**: camelCase (`userName`, `handleClick`)
- **클래스/인터페이스**: PascalCase (`UserInfo`, `ApiResponse`)
- **상수**: UPPER_SNAKE_CASE (`MAX_LENGTH`)
- **파일**: PascalCase.svelte (`UserProfile.svelte`)

### 코드 스타일
- **들여쓰기**: 2칸 스페이스
- **따옴표**: 큰따옴표 사용
- **세미콜론**: 필수
- **trailing commas**: 사용 안함

### Svelte 5 규칙
- `$state`, `$derived` rune 적극 활용
- 디자인 서버 CSS 클래스 우선 사용
- 컴포넌트는 최소 단위로 분리
- Props는 단순하게 유지

## 다국어 처리

### 지원 언어
- **ko**: 한국어 (기본)
- **en**: 영어
- **ja**: 일본어
- **vi**: 베트남어
- **zh**: 중국어

### 파일 구조
```
static/resources/i18n/
├── commonMessages_ko.json    # 공통 메시지
├── emlMessages_ko.json       # 전자우편 메시지
├── msgrMessages_ko.json      # 메신저 메시지
└── ... (모듈별 메시지 파일)
```

### 키 네이밍 규칙
- **포맷**: `{namespace}.{type}.{camelCaseKey}`
- **타입**: `label` (라벨), `text` (본문), `error` (에러), `guide` (도움말)
- **예시**: `eml.label.selectMailbox`, `eml.text.pleaseSelectUser`

### 사용법
```typescript
import { I18n } from '$lib/common/i18n';
I18n.get('eml.text.selectUser', { default: '사용자를 선택해 주세요' })
```

## AI 작업 지침

### 기본 원칙
- **항상 한국어로 응답**
- **모호한 지시는 반드시 확인 요청**
- **추측하지 말고 명확히 확인**
- **2단계 절차**: 의도 확인 → 작업 실행

### 다국어 작업 시 주의사항
- 기존 JSON 키-값 수정 금지 (추가만 가능)
- 중복 키 생성 금지
- 완전 일치만 인정 (부분 일치 불허)
- REF 번역 우선 활용

## 테스트

### 테스트 프레임워크
- **Playwright**: E2E 테스트
- **Vitest**: 단위 테스트

### 테스트 케이스
`테스트케이스 계획서/` 디렉토리에 모듈별 테스트 계획서 보관:
- EML (전자우편) 테스트 케이스
- 사용자 설정, 목록, 보기, 쓰기 등 기능별 테스트

## 주요 설정 파일

### .cursor-instructions.md
- AI 작업을 위한 상세 지침
- 한국어 응답 필수
- 의도 확인 절차 강제

### .cursorrules
- 코딩 스타일 및 아키텍처 규칙
- i18n 처리 규칙
- Svelte 5 컨벤션

### .vscode/settings.json
- ESLint, Prettier 설정
- Svelte 지원 설정
- i18n-ally 플러그인 설정

## 라이선스
ISC

---
*이 문서는 프로젝트 분석을 통해 생성되었습니다.*