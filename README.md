# AirGap Repo Design Doc Writer

> 레포 전체 설계/아키텍처 문서를 자동 생성하는 OpenClaw Agent Skill.
> 폐쇄망(에어갭)의 내부 코딩 에이전트와 개발자가 인터넷·외부 문서 없이도 코드베이스를 이해하도록 만든다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://docs.openclaw.ai)

## 🎯 무엇을 하는가

단일 기능이 아니라 **시스템 전체** — 레이어 구조, 모든 서비스/컴포넌트, 데이터 흐름, 의존 외부 서버(DB·큐·캐시·오브젝트스토어·모델서버·게이트웨이 등) 토폴로지를 **한 장의 설계도**로 만든다.

- 👤 **사람용**: 개발자 온보딩, 시스템 이해, 아키텍처 리뷰
- 🤖 **에이전트용**: 폐쇄망의 코딩 에이전트가 오프라인에서 코드베이스를 자립적으로 이해

## ✨ 핵심 기능

| 기능 | 설명 |
|---|---|
| **전체 레포 스캔** | 매니페스트, 디렉터리 구조, 엔트리포인트, Dockerfile, CI, k8s/compose 매니페스트 등 |
| **컴포넌트 인벤토리** | 모듈/패키지별 책임 표 — 핵심 추상화(인터페이스/DI)와 구체 구현 구분 |
| **외부 서버 토폴로지** | 설정·클라이언트·배포 교차 확인 → 서버/프로토콜/포트/용도/필수여부 표 + ASCII 다이어그램 |
| **핵심 데이터 흐름** | 대표 요청 경로 2~4개 端到端 분석 (동기/비동기 구분) |
| **횡단 관심사** | 설정/시크릿, 인증, 로깅/관측, 동시성, 에러/재시도, 배포/롤아웃 |
| **"왜" 복원** | git log/blame/PR에서 비자명한 구조 결정의 근거 캐서 설명 |

## 📋 산출물

```
docs/design/architecture.md   ← 완성된 설계 문서 (또는 레포 관례 위치)
```

## 🚀 사용법

### OpenClaw Agent Skill로 설치

```bash
openclaw skills install junnystateofmind/airgap-repo-design-doc-writer
```

### 에이전트에게 요청

```
이 레포 전체 설계 문서 써줘
아키텍처/온보딩 문서 만들어줘
내부 에이전트가 코드베이스 이해하게 정리해줘
시스템이 어떤 서버들에 의존하는지 확인해줘
새 개발자가 보고 이해할 설계서 만들어줘
```

## 📐 생성 문서 구조

생성되는 설계 문서는 다음 섹션을 포함한다:

```markdown
1. 개요              - 시스템 한 줄 요약
2. 레이어 구조      - API → 서비스 → 도메인 → ...
3. 컴포넌트 인벤토리 - 모듈별 책임 테이블
4. 외부 서버 토폴로지 - 연결 다이어그램 + 테이블
5. 핵심 데이터 흐름   - 端到端 흐름 (동기/비동기)
6. 횡단 관심사       - 설정/인증/관측/동시성/에러/배포
7. 주요 설계 결정     - git 히스토리 기반 "why"
8. 빌드·실행·테스트   - 기동 방법
9. Known Gaps        - 미확인 사항 및 주의점
```

전체 템플릿은 [`templates/design-doc.md`](templates/design-doc.md) 참고.

## ⚙️ 작성 원칙

1. **시스템 전체를 균형 있게** — 최근 커밋이나 한 기능에 끌려가지 않음
2. **의존 서버를 빠짐없이** — 설정/클라이언트/배포 교차 확인
3. **"왜"를 git에서** — 비자명한 구조는 `git log`/`blame`/PR로 근거 검증
4. **검증된 사실만** — 포트/버전/엔드포인트는 코드·설정에서 확인, 추측은 추측으로 표기

## 📁 프로젝트 구조

```
airgap-repo-design-doc-writer/
├── SKILL.md              # 스킬 정의 (agent prompt)
├── agents/
│   └── openai.yaml       # 에이전트 인터페이스 정의
├── templates/
│   └── design-doc.md     # 산출물 템플릿
└── README.md
```

## 🔗 관련

- [OpenClaw Docs](https://docs.openclaw.ai)
- [OpenClaw Skill Development](https://docs.openclaw.ai/skills)
- [Hermes Agent Skill](https://github.com/junnystateofmind/hermes)

## 📄 License

MIT
