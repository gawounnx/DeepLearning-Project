# skills-security-review

- 대상: 프로젝트 스킬 4종 — `verification-before-completion`, `finishing-a-development-branch`(obra/superpowers), `code-review`, `setup-matt-pocock-skills`(mattpocock/skills)
- 검토 기준: Harness §4-6 (출처, 본문·동봉 파일 검토, 버전 고정, 권한 최소화), §4-3 점검 체크리스트 7번
- 작성·검토: Claude Code (Claude Sonnet 5.5). 다른 계열 모델과 사람 리뷰는 아직 없음
- 검토일: 2026-11-08
- 검토한 커밋: obra/superpowers `22f0b463e7a5e579904dd6211a520321035526f7`(v7.0.2), mattpocock/skills `4ae2317ddb22b046e26455e4f9c9b3aaaf62212d`
- 변경 위험: 보통 (에이전트가 따르는 지시문 추가. 코드·공통 파일 변경 없음)

## 검토 방법

1. 두 저장소를 격리 폴더에 `--depth 1`로 받아 위 커밋을 확인했다.
2. 4개 스킬의 `SKILL.md`와 동봉 파일 전체(마크다운 6개, yaml 2개)를 읽었다. 스크립트 파일은 없다.
3. 위험 신호(외부 URL, `curl`·`wget`, `.env`·`.ssh`·자격 증명, base64·`eval`, 추가 설치 지시, 권한 설정 변경)를 grep으로 훑었다.
4. 보이지 않는 유니코드(zero-width, 방향 제어, 사설 영역)를 검사했다.
5. `npx skills add --copy`로 설치한 뒤, 설치된 파일을 검토한 커밋의 파일과 SHA-256으로 비교했다. `.agents/skills/`와 `.claude/skills/` 모두 일치했다.

## 결과

| 지적 사항 | 근거 | 심각도 | 반영 여부 | 비고 |
| --- | --- | --- | --- | --- |
| 위험 신호 없음 (4종 공통) | 외부 전송·자격 증명 접근·난독화·추가 설치 지시·권한 변경 없음. 보이지 않는 문자 0건. 외부 URL은 `setup-matt-pocock-skills`의 `glab` CLI 링크 2곳뿐 | - | 해당 없음 | 설치 도구의 위험 평가도 Gen·Socket·Snyk 모두 Safe 또는 낮음. `code-review`만 Snyk Med Risk (아래) |
| `setup-matt-pocock-skills`가 `CLAUDE.md`가 있으면 거기에 `## Agent skills` 블록을 씀 | 본문 §4 "If `CLAUDE.md` exists, edit it" | 중요 | 미반영: 실행하지 않음 | AGENTS.md §9·Harness §4-3 ①은 블록을 `AGENTS.md`에 두라고 함. 실행 전에 `AGENTS.md`에 쓰도록 지정하고 두 사람이 합의해야 함. `disable-model-invocation: true`라 자동 호출되지 않음 |
| 같은 스킬이 로컬 `GLOSSARY.md`를 저장소 루트에서 찾음 | `domain.md`. 이 프로젝트의 용어집은 `docs/GLOSSARY.md` | 사소 | 미반영 | 없으면 조용히 넘어가는 규칙이라 동작은 막히지 않으나, 실행 시 용어집·ADR 위치를 `docs/GLOSSARY.md`, `docs/adr/`로 지정해야 함 |
| `code-review`가 서브에이전트를 병렬 실행하고 이슈 트래커 문서를 전제함 | 본문 §4, "tell the user to run `/setup-matt-pocock-skills`" | 사소 | 미반영 | 읽기 전용 검토 지시라 위험 신호는 아님. Snyk Med Risk는 서브에이전트 위임 때문으로 추정되나 확인하지 않음. Codex에서 두 축이 분리되어 나오는지 처음 한 번 확인 필요(Harness §4-3 ⑥) |
| `code-review`가 내장 `/code-review`와 이름이 같음 | Claude Code 스킬 목록 | 사소 | 미반영 | 프로젝트 스킬 호출 시 어느 쪽이 실행되는지 첫 사용 때 확인 |
| 이슈 트래커 템플릿(GitHub·GitLab)이 `gh`·`glab`로 이슈 생성·라벨 생성을 지시 | `issue-tracker-github.md` | 사소 | 미반영 | 실행 시에 사용자 확인을 거침(본문 §3). 이 프로젝트에서 트래커를 정하는 것은 사람의 결정 |

## 아직 하지 않은 것

- 세 에이전트(Claude Code·Codex·Antigravity)에서 스킬 인식과 호출 확인 (Harness §3 ⑤)
- `scripts/sync_skills.py`와 `--check` (이 저장소에 아직 없음. 지금은 `npx skills add --copy`가 두 폴더를 같은 내용으로 만듦)
- Skills 표·설치 결정 ADR (AGENTS.md §2: ADR은 두 사람의 합의 필요)
