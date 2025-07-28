---
description: 다국어(i18n) 파일 작업 시 사용하는 상세 규칙
globs: *.svelte,*.ts,commonMessages_*.json,emlMessages_*.json
alwaysApply: false
---

# 다국어(i18n) 처리 규칙
## 🚨 절대 규칙
- ❌ **기존 JSON 키-값 수정 금지** - 추가만 가능
- ❌ **중복 키 생성 금지**
- ❌ **단어 분할 검색 절대 금지** - 완전한 문장 단위로만 매칭
- ✅ **완전 일치만 인정** - 부분 일치/유사 표현은 불일치


## 🌍 기본 설정
- **기본 경로**: [emlMessages_ko.json](mdc:packages/naon-webapp/static/resources/i18n/emlMessages_ko.json) 가 포함된 디렉토리
- **지원 언어**: ko(한국어), en(영어), ja(일본어), vi(베트남어), zh(중국어)
- **파일 패턴**: `{namespace}Messages_{lang}.json`

## 🔍 우선순위 검색 순서 (절대 준수)
1. [commonMessages_ko.json](mdc:packages/naon-webapp/static/resources/i18n/commonMessages_ko.json)
2. [emlMessages_ko.json](mdc:packages/naon-webapp/static/resources/i18n/emlMessages_ko.json)




## 🏷️ 키 네이밍 규칙
- **포맷**: `{namespace}.{type}.{camelCaseKey}`
- **예시**: 
  - `"메일함 선택"` → `eml.label.selectMailbox`
  - `"사용자를 선택해 주세요"` → `eml.text.pleaseSelectUser`

### Type 분류:
- `label`: UI 라벨, 버튼 텍스트
- `text`: 본문, 메시지, 안내문  
- `error`: 에러 메시지
- `guide`: 도움말, 가이드

## 📋 표준 작업 절차
1. **하드코딩 한글 수집** - `"텍스트"` 형태 탐지
2. **우선순위 매칭** - 1~6단계 순서대로 확인
3. **기존 키 확인** - 동일 한글 값 키 존재 확인
4. **REF 번역 활용** - 존재 시 5개 언어 모두 복사
5. **신규 키 생성** - 6단계일 경우만, 한글 그대로 입력
6. **작업 계획 보고서 생성** (자동)
7. **사용자 승인 대기** - "진행해" 명령 후 편집 시작
8. **소스 코드 치환**
9. **import 확인 및 추가**
10. **JSON 파일 추가** - 마지막 줄에만

## 💻 코드 적용 방식
### Svelte / TypeScript:
```typescript
import { I18n } from '$lib/common/i18n';
I18n.get('eml.text.selectUser', { default: '사용자를 선택해 주세요' })
```

## 📊 보고서 형식
| 한글 텍스트 | 우선순위 | 참조된 키 | 최종 키 | 상태 | 비고 |
|------------|---------|----------|---------|------|------|
| 메일함 선택 | 3 | eml.label.selectMailbox | eml.label.selectMailbox | 재사용 | REF에서 번역 복사 |
| 이름을 입력해 주세요 | 6 | - | eml.text.enterName | 신규 | 번역 없음 |

## ✅ 체크리스트
- [ ] AI가 직접 번역하지 않았는가?
- [ ] 기존 JSON을 변경하지 않았는가?  
- [ ] 키가 중복되지 않았는가?
- [ ] REF/기존 키 우선 사용했는가?
- [ ] default 값 포함했는가?
- [ ] import 누락되지 않았는가?
- [ ] 승인 후 편집을 시작했는가?
