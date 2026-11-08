# LawLens

약관·계약 문서(PDF·DOCX)에서 당사자·권리·의무 관계를 그래프로 보여주고, 약관의 불리할 수 있는 조항을 원문 근거·판단 근거와 함께 표시하는 문서 분석 보조 도구.

> 심층학습 기말 프로젝트 · 2026-11-08 ~ 2026-12-14(최종 발표) · 배포 없음, Lab 서버 + SSH 라이브 데모
> 이 서비스는 법률 자문이 아니며 위법 여부를 확정하지 않습니다.

## 문서

| 문서 | 내용 |
|---|---|
| [SPEC.md](SPEC.md) | 요구사항 명세서 |
| [GLOSSARY.md](GLOSSARY.md) | 도메인 용어집 (코드·문서 용어의 기준) |
| [adr/](adr/) | 결정 기록 (ADR 0001~0005) |

## 디렉터리 구조

```
├── backend/            FastAPI 분석 서비스
│   ├── app/
│   │   ├── api/        API 엔드포인트
│   │   ├── ingestion/  문서 수집·파싱 (DOCX→PDF 변환, 조항 분할)
│   │   ├── judgment/   불리 판정 (추론, 표시 단계 결정)
│   │   ├── retrieval/  참조 사례 검색
│   │   ├── summary/    판단 근거 요약
│   │   ├── relations/  관계 추출 (EXAONE, 응답 처리, 원문 검증)
│   │   ├── graph/      그래프 구성
│   │   └── pipeline/   비동기 분석 작업·상태
│   └── tests/          분석 서비스 경계 테스트 (fixtures/에 샘플 문서)
├── frontend/           React + Vite + TypeScript (뷰어 + Cytoscape 그래프)
├── ml/                 학습·실험
│   ├── data_check/     1주 차 데이터 점검
│   ├── classifier/     L0·E0~E3, 관련 조문 모델
│   ├── calibration/    온도 스케일링 + Mondrian Conformal
│   ├── retrieval/      참조 사례 색인 생성
│   ├── eval/           평가 하네스 (E0~E3, E5)
│   └── configs/        실험 설정
├── data/
│   ├── raw/            AI Hub 원본 (커밋 금지)
│   ├── processed/      가공 데이터 (커밋 금지)
│   ├── gold/           관계 정답셋·주석 가이드 (커밋)
│   └── demo/           데모용 공개 약관 (커밋)
├── models/             학습된 체크포인트 (커밋 금지)
├── scripts/            Lab 서버 실행 스크립트 (vLLM 서빙 등)
├── .agents/skills/     Codex·Antigravity용 프로젝트 스킬
└── .claude/skills/     Claude Code용 프로젝트 스킬
```

## 팀

- 고용민 — ML·백엔드 (`ml/`, `backend/app/{judgment,retrieval,summary,pipeline,api}`)
- 차가원 — 문서·프론트 (`backend/app/{ingestion,relations,graph}`, `frontend/`)

## 개발 환경

- Lab 서버: RTX 5090 (CUDA 12.8 이상, PyTorch 2.7 이상)
- 실행·설치 방법: 패키지 관리 도구 확정 후 작성 예정
