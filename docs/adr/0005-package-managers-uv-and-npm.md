# 패키지 관리 도구는 Python uv, Node npm으로 통일한다

재현 가능한 개발 및 실행 환경을 보장하기 위해 Python 패키지 관리 도구는 `uv`, 프론트엔드 Node 패키지 관리 도구는 `npm`으로 통일한다. Python에서 `uv`는 빠른 패키지 설치와 `uv.lock`을 통한 결정론적 의존성 고정을 지원하며, 가상환경 및 Python 인터프리터 버전 관리를 일원화할 수 있다. 프론트엔드는 단일 Vite SPA 구조이므로 별도의 추가 도구 설치 없이 Node 기본 제공 도구인 `npm`(`package-lock.json`)을 사용하여 설정 복잡성을 최소화한다.

## Consequences

- 백엔드·ML 개발 및 의존성 관리는 루트 `pyproject.toml`과 `uv.lock`을 기준으로 한다.
- 프론트엔드는 `frontend/package.json`과 `package-lock.json`으로 관리하며, npm 기반 Vite 템플릿으로 초기화한다.
- Lab 서버의 EXAONE 서빙용 vLLM 환경은 의존성 충돌(PyTorch 및 transformers 버전 고정 요건)을 방지하기 위해 백엔드/ML 환경과 분리된 독립 가상환경(`scripts/` 등)으로 운용할 수 있다.
- 모든 팀원은 임의의 도구(conda, poetry, pnpm, yarn 등)를 혼용하지 않으며, 의존성 변경 시 잠금 파일(`uv.lock`, `package-lock.json`)을 반드시 함께 커밋한다.
