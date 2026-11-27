# .github

# 워크크 (WCC) — 개발 가이드

MS 5기 1차 팀 프로젝트 **워크크**의 협업 규칙과 개발 가이드입니다.
모든 팀원은 작업 전에 이 문서를 확인해 주세요.

---

## Repository 구성

| Repository | 설명 | 기술 스택 | 배포 |
|---|---|---|---|
| `Meoning-Reosin-frontend` | 웹 화면 | Next.js | Vercel |
| `Meoning-Reosin-backend` | API 서버 | FastAPI, PostgreSQL | GitHub Actions → ACR → ACA |
| `Meoning-Reosin-ai` | 사진 인식, 데이터 준비 | Azure AI Vision, Azure OpenAI | Blob Storage |
| `Meoning-Reosin-infra` | 인프라 설정, 문서 | Azure | - |

---

## 협업 흐름 (Workflow)

1. **이슈 생성**: Projects 보드 → `+ Add item` → `Create new issue` → 레포 선택
   - 라벨(파트 + 종류), Priority 지정
2. **브랜치 생성**: 이슈 오른쪽 `Development` → `Create a branch` → 카드를 `In Progress`로
3. **작업 및 커밋**: 커밋 컨벤션에 맞춰 커밋
4. **PR 생성**: `main` 대상, 본문에 `Closes #이슈번호` → 카드를 `Review`로
5. **코드 리뷰**: 팀원 1명 이상 확인
6. **병합**: `Squash and merge` → 브랜치 자동 삭제 → 이슈와 카드 자동 `Done`

> `main` 브랜치에는 직접 push할 수 없습니다. 모든 변경은 PR로 올려 주세요.

---

## 브랜치 전략

`main` 하나와 작업 브랜치로 운영합니다 (GitHub Flow).

| 브랜치 | 용도 | 예시 |
|---|---|---|
| `main` | 배포되는 최신 코드 | - |
| `feat/*` | 새 기능 | `feat/recognize-api` |
| `fix/*` | 버그 수정 | `fix/login-error` |
| `docs/*` | 문서 | `docs/readme` |
| `chore/*` | 설정, 빌드, 기타 | `chore/dockerfile` |

- 브랜치 이름은 **영어 소문자 + 하이픈(-)** 을 사용합니다.

---

## 커밋 컨벤션

[Conventional Commits](https://www.conventionalcommits.org/) 형식을 따릅니다.

```
<type>: <subject>
```

| type | 의미 |
|---|---|
| `feat` | 새로운 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 수정 |
| `style` | 코드 포맷, 세미콜론 등 (동작 변화 없음) |
| `refactor` | 리팩토링 (기능 변화 없음) |
| `test` | 테스트 코드 추가·수정 |
| `chore` | 빌드, 설정, 패키지 등 기타 |

**예시**

'''
feat: 장소 추천 API 추가
fix: 사진 업로드 시 500 오류 수정
docs: 백엔드 실행 방법 추가
chore: Dockerfile Python 3.12로 변경
'''

- subject는 50자 이내, 마침표 없이 작성합니다.
- PR 제목도 같은 형식으로 작성합니다 (Squash merge 시 PR 제목이 커밋 메시지가 됩니다).

---

## 라벨

| 구분 | 라벨 |
|---|---|
| 파트 | `frontend` `backend` `ai` `infra` |
| 종류 | `feat` `bug` `docs` `chore` |

Priority(`High` / `Medium` / `Low`)는 Projects 보드 필드로 지정합니다.

---

## 코드 리뷰 규칙

- PR은 **작게** 올립니다 (기능 하나 단위).
- 리뷰어는 가능하면 **당일 안에** 확인합니다.
- 리뷰 코멘트는 존중하는 말투로, 이유와 함께 작성합니다.
- 리뷰 반영 후 대화(conversation)를 Resolve합니다.

---

## 보안 규칙

- `.env`, API 키, 비밀번호, 연결 문자열은 **절대 커밋하지 않습니다.**
  - 필요한 변수 이름은 `.env.example`에 값 없이 적습니다.
  - 실제 값은 각자 로컬 `.env`와 Azure Container Apps 시크릿에만 둡니다.
- 데이터셋(AI Hub 등)과 사진은 GitHub이 아닌 **Azure Blob Storage**에 올립니다.
- 키가 실수로 커밋되었다면 **즉시 공유하고 키를 재발급**합니다.
- Secret scanning과 Push protection이 켜져 있어 키가 포함된 push는 차단됩니다.

---

## 개발 환경

| 도구 | 버전 | 대상 |
|---|---|---|
| Git, VS Code | 최신 | 전원 |
| Node.js | LTS | 프론트 |
| Python | **3.12** | 백엔드, AI |
| Docker Desktop | 최신 | 백엔드, AI, 인프라 |
| Azure CLI, azcopy, DBeaver | 최신 | 인프라 (필요 시 AI) |

각 레포의 실행 방법은 해당 레포 `README.md`를 참고해 주세요.

---

## 소통

- 작업 관련 질문과 논의는 **해당 이슈·PR 댓글**에 `@아이디`로 남깁니다.
- 각 레포 오른쪽 위 `Watch` → `All Activity`로 알림을 받습니다.
- 대화방에서 결정한 내용은 아래 **공지**에 기록합니다.

---

## 일정

| 기간 | 목표 |
|---|---|
| ~ 11/27 | 1차 프로토타입, 서버 첫 배포 (`/health`) |
| ~ 11/29 | 파트별 기능 개발 |
| ~ 12/1 | MVP 완성 |
| ~ 12/4 | 확장 기능 완성 |
| 12/8 | 최종 발표 |

---

## 공지

- **11/27** GitHub 협업 설정 완료. 이슈는 Projects 보드에서 생성해 주세요.
