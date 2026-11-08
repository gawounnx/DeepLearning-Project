# Third-Party Notices

이 저장소에는 아래 오픈소스 에이전트 스킬이 **수정 없이 그대로** 포함되어 있다.
각 스킬의 저작권과 라이선스는 원저작자에게 있으며, 해당 라이선스 조건에 따라 재배포한다.
LawLens 프로젝트 자체의 코드·문서는 이 고지의 대상이 아니다.

- 설치 위치: `.agents/skills/<이름>/` (Codex·Antigravity용), `.claude/skills/<이름>/` (Claude Code용). 두 위치의 내용은 동일하다.
- 설치 도구: `npx skills add --copy` (skills CLI 1.7.6), 설치일 2026-11-08
- 내용 무결성: [skills-lock.json](skills-lock.json)의 `computedHash`가 설치 시점의 내용 해시다.
- 변경 사항: **없음** (원본 파일을 수정하지 않았다).
- 라이선스 전문: [third_party_licenses/](third_party_licenses/)

| 스킬 | 원본 저장소 | 원본 경로 | 라이선스 | 저작권 표기 |
|---|---|---|---|---|
| fastapi | https://github.com/fastapi/fastapi | `.agents/skills/fastapi` | MIT | Copyright (c) 2018 Sebastián Ramírez |
| playwright-cli | https://github.com/microsoft/playwright-cli | `skills/playwright-cli` | Apache-2.0 | Copyright (c) Microsoft Corporation |
| vercel-react-best-practices | https://github.com/vercel-labs/agent-skills | `skills/react-best-practices` | MIT (원저작자 선언) | Vercel Engineering (아래 참고) |
| verification-before-completion | https://github.com/obra/superpowers | `skills/verification-before-completion` | MIT | Copyright (c) 2025 Jesse Vincent |
| finishing-a-development-branch | https://github.com/obra/superpowers | `skills/finishing-a-development-branch` | MIT | Copyright (c) 2025 Jesse Vincent |
| code-review | https://github.com/mattpocock/skills | `skills/engineering/code-review` | MIT | Copyright (c) 2026 Matt Pocock |
| setup-matt-pocock-skills | https://github.com/mattpocock/skills | `skills/engineering/setup-matt-pocock-skills` | MIT | Copyright (c) 2026 Matt Pocock |

## 라이선스 전문

- fastapi → [third_party_licenses/fastapi-LICENSE.txt](third_party_licenses/fastapi-LICENSE.txt)
- playwright-cli → [third_party_licenses/playwright-cli-LICENSE.txt](third_party_licenses/playwright-cli-LICENSE.txt) (Apache License 2.0 전문. 원본 저장소에 NOTICE 파일은 없다.)
- vercel-react-best-practices → [third_party_licenses/vercel-react-best-practices-LICENSE.txt](third_party_licenses/vercel-react-best-practices-LICENSE.txt)
- verification-before-completion, finishing-a-development-branch → [third_party_licenses/superpowers-LICENSE.txt](third_party_licenses/superpowers-LICENSE.txt)
- code-review, setup-matt-pocock-skills → [third_party_licenses/mattpocock-skills-LICENSE.txt](third_party_licenses/mattpocock-skills-LICENSE.txt)

## 참고 사항

- **추가 4종(2026-11-08)**: 설치 전 `SKILL.md`와 동봉 파일 전체를 검토했다. 검토한 커밋은 obra/superpowers `22f0b463e7a5e579904dd6211a520321035526f7`, mattpocock/skills `4ae2317ddb22b046e26455e4f9c9b3aaaf62212d`이며, 설치된 파일은 이 커밋의 파일과 SHA-256이 일치한다. 검토 기록은 [docs/reviews/skills-security-review.md](docs/reviews/skills-security-review.md).
- **setup-matt-pocock-skills**: 설치만 했고 실행하지 않았다. 실행하면 `CLAUDE.md`가 있을 때 `CLAUDE.md`에 `## Agent skills` 블록을 쓰므로(AGENTS.md §9·Harness §4-3 ①과 충돌) 실행 전에 `AGENTS.md`에 쓰도록 지정하고 두 사람이 합의해야 한다.

- **vercel-react-best-practices**: 원본 저장소는 LICENSE 파일과 저작권자·연도 표기를 두지 않고, README의 License 항목과 SKILL.md 머리말(`license: MIT`)에서 MIT라고만 밝힌다. 이 고지는 그 선언을 그대로 따르며, 저작권자 이름은 임의로 적지 않았다. 원저작자가 LICENSE 파일을 추가하면 그 내용으로 교체한다.
- **상표**: FastAPI, Playwright, Microsoft, Vercel 등 이름과 로고는 각 권리자의 상표이며, 이 저장소는 해당 권리자와 제휴하거나 보증받지 않았다.
- **외부 서비스**: fastapi 스킬은 FastAPI Cloud(유료 호스팅) 배포를 제안하는 문구를 포함한다. LawLens는 배포를 하지 않으므로(SPEC 범위 밖) 이 기능을 사용하지 않는다.
- **무보증**: 각 라이선스에 따라 스킬은 "있는 그대로" 제공되며, 보증 책임은 지지 않는다.
