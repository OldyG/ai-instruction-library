---
description: 
globs: 
---

# 나온 프로젝트 구조 및 목적

## 🎯 프로젝트 목적
- **Spring + JSP에서 Svelte 5로 전환 중인 그룹웨어 시스템**
- UI 단일 서버에서 각종 API 서버로 요청 처리하는 아키텍처

## 📁 핵심 디렉토리 구조
```
/packages/naon-webapp/
├── src/
│   ├── lib/
│   │   ├── api/           # API 클라이언트 (ModuleCode별)
│   │   ├── biz/           # 비즈니스 로직 (ModuleCode별)
│   │   ├── common/        # 공통 유틸리티
│   │   ├── constants/     # 상수 정의
│   │   └── enum/common/   # ModuleCode 타입 정의
│   └── routes/[[header]]/ # 라우트 (ModuleCode별)
├── static/resources/
│   ├── i18n/             # 다국어 리소스
│   ├── images/           # 이미지 리소스
│   └── styles/           # 스타일 리소스
```

## 🔧 ModuleCode 기반 구조
- `/lib/enum/common/CmmEnum`에 `ModuleCode` 타입 정의
- 모든 모듈은 이 코드에 맞춰 폴더 구성:
  - `/lib/api/{ModuleCode}`
  - `/lib/biz/{ModuleCode}` 
  - `/routes/[[header]]/{ModuleCode}`


## 🌍 다국어 리소스
- **기본 경로**: `/packages/naon-webapp/static/resources/i18n`
- **지원 언어**: ko, en, ja, vi, zh
- **파일 패턴**: `{namespace}Messages_{lang}.json`
- **우선순위**: commonMessages → emlMessages → REF 파일들

## 🎨 스타일링 시스템
- **디자인 서버 CSS** 우선 사용
- **최상위 layout**에서 CSS 로드
- **퍼블리셔 제공 클래스** 활용: `btn`, `input_txt`, `tbl_basic` 등
- **컴포넌트 내 `<style>` 태그는 기본적으로 지양**

## 🔗 URL 패턴
- 파일 기반 라우팅 (SvelteKit)
- `[[header]]` 패턴으로 헤더 유무 선택적 처리
- 각 모듈별 URL Builder 클래스로 URL 생성 관리
