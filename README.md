# 프론트엔드 엔지니어 박수범

비즈니스 문제를 기술의 언어로 풀고, 포용적인 인터페이스로 누구나 소외되지 않는 웹을 만듭니다. 단순히 기능을 구현하는 것을 넘어 문제 정의에서 가설 검증, 운영까지 이어지는 흐름 속에서 실질적인 임팩트를 만들어내는 데 집중합니다.

<a href="https://subeomdev.vercel.app/blog"><img src="https://img.shields.io/badge/Tech_Log-20C20E?style=for-the-badge&logo=tistory&logoColor=white" alt="Blog"/></a>
<a href="https://subeomdev.vercel.app/"><img src="https://img.shields.io/badge/Portfolio-443E38?style=for-the-badge&logo=react&logoColor=white" alt="Portfolio"/></a>

---

## Featured Projects

### Claude Skills Panel — VSCode / Cursor 확장 프로그램

Open VSX Registry에 게시한 오픈소스 익스텐션입니다. VSCode, Cursor, VSCodium 등 Open VSX 호환 IDE에서 사용할 수 있습니다.

<p align="center">
  <a href="https://open-vsx.org/extension/parksubeom/claude-skills-panel">
    <img src="https://img.shields.io/open-vsx/v/parksubeom/claude-skills-panel?style=for-the-badge&label=Open%20VSX&color=c160ef&logo=eclipseide&logoColor=white" alt="Open VSX Version"/>
  </a>
  <a href="https://open-vsx.org/extension/parksubeom/claude-skills-panel">
    <img src="https://img.shields.io/open-vsx/dt/parksubeom/claude-skills-panel?style=for-the-badge&label=Downloads&color=20C20E" alt="Downloads"/>
  </a>
  <a href="https://open-vsx.org/extension/parksubeom/claude-skills-panel">
    <img src="https://img.shields.io/badge/Install-Open%20VSX에서%20설치-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" alt="Install"/>
  </a>
</p>

> **▶ [Open VSX에서 바로 설치하기](https://open-vsx.org/extension/parksubeom/claude-skills-panel)** &nbsp;·&nbsp; Publisher: `parksubeom.claude-skills-panel`

**해결한 문제**

Anthropic이 발표한 Claude Skills(SKILL.md 기반 작업별 지침 모음)는 강력하지만, 어떤 스킬이 활성화돼 있는지 추적하려면 매번 `~/.claude/skills` 디렉토리를 직접 뒤져야 했습니다. 글로벌과 워크스페이스 스킬을 한눈에 보고 토글로 관리할 수 있는 도구를 직접 만들어 출시했습니다.

**핵심 기능**
- 워크스페이스(`.claude/skills`)와 글로벌(`~/.claude/skills`) 스킬을 하나의 사이드 패널에서 Tree View로 시각화
- SKILL.md를 직접 편집하지 않고도 GUI에서 원클릭 활성/비활성 토글
- frontmatter의 `name`/`description`을 트리뷰 tooltip에 자동 표시
- 디바운스된 파일 워처로 외부 스킬 추가/삭제를 실시간 반영

<table>
  <tr>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/1664892d-942e-4c51-80d8-93fc7d471c95" alt="스킬 토글 동작"/>
    </td>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/9cc877b4-097e-4eda-a001-b4af14620b70" alt="frontmatter tooltip 표시"/>
    </td>
  </tr>
</table>

**기술적 의사결정**
- VSCode Extension API + TypeScript 기반, TreeDataProvider 패턴으로 lazy loading 및 캐시 무효화 일원화
- 초기 `fs.watch`의 Linux recursive 미지원 및 atomic save 미감지 문제를 chokidar로 마이그레이션하고 150ms debounce로 burst 이벤트 통합
- `workspaceState`(프로젝트별)와 `globalState`(전역)를 분리해 상태 영속화하고 프로젝트 간 누수 차단
- 토글 명령을 `enable`/`disable` 두 멱등 명령으로 분리해 빠른 연타에서도 race condition 방지
- 외부 SKILL.md 컨텐츠를 신뢰하지 않도록 `MarkdownString.isTrusted = false`로 명시해 의도치 않은 명령 실행 차단

**의의**

AI 코딩 도구 생태계의 실사용 문제를 직접 정의하고 도구로 해결해 publisher(`parksubeom.claude-skills-panel`)로 정식 배포한 사례입니다.

---

### claude-distill — Claude Code 세션 지식 자동 축적 CLI

Claude Code 세션이 끝날 때마다 트랜스크립트를 분석해 배운 것(`knowledge.md`)과 실수·함정(`gotchas.md`)을 자동으로 누적하는 Hook 기반 피드백 루프입니다. "매일 새로 출근하는 알바생" 같던 AI가 다음 세션에는 지난 세션의 교훈을 알고 시작하도록, 같은 설명을 반복할 필요를 없앱니다.

<p align="center">
  <a href="https://www.npmjs.com/package/claude-distill">
    <img src="https://img.shields.io/npm/v/claude-distill?style=for-the-badge&label=npm&color=c160ef&logo=npm&logoColor=white" alt="npm Version"/>
  </a>
  <a href="https://www.npmjs.com/package/claude-distill">
    <img src="https://img.shields.io/npm/dt/claude-distill?style=for-the-badge&label=Downloads&color=20C20E&logo=npm&logoColor=white" alt="npm Downloads"/>
  </a>
  <a href="https://github.com/parksubeom/claude-distill">
    <img src="https://img.shields.io/badge/Repo-claude--distill-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repository"/>
  </a>
</p>

> **▶ [npm에서 보기](https://www.npmjs.com/package/claude-distill)** &nbsp;·&nbsp; 설치: `npm install -g claude-distill && claude-distill init`

**해결한 문제**

Claude Code는 세션이 바뀌면 지난 대화에서 발견한 환경 특성·API 함정·의사결정을 기억하지 못해, 매번 같은 맥락을 다시 설명해야 했습니다. 세션 종료 시 트랜스크립트를 분석해 재사용할 지식과 반복하면 안 될 실수를 markdown으로 자동 축적하고, 다음 세션이 이를 참조하게 만들었습니다.

**핵심 기능**
- Stop hook으로 세션 종료 시 자동 분석 — `knowledge.md`(판례)·`gotchas.md`(사고) 두 파일에 누적
- 발견한 내용을 11종 카테고리(trade-off 결정·환경 특성·API 함정·동시성 이슈 등)로 분류
- 트랜스크립트에서 한글 비율을 감지해 한/영 자동 전환(`CLAUDE_DISTILL_LANG`로 강제 가능)
- 결과가 순수 markdown이라 사용자가 직접 편집·삭제 가능하고, 삭제한 항목은 다음 세션에 주입되지 않음

**기술적 의사결정**
- **다단계 게이트**로 비용 최적화: 휴리스틱(무료) → Haiku 단일 토큰 yes/no 판정 → dedup 해시 → 재귀 가드 순으로 걸러, 세션의 약 90%가 값비싼 Sonnet 분석 전에 종료 — 본 추출 호출 **~10× 컷**
- 대부분 세션은 **~$0**, 게이트를 통과한 세션만 **~$0.10**(Sonnet 입력 ~20K·출력 ~2K 토큰) 수준으로 운영비 통제
- **프라이버시 우선** — 제3자 서버 없이 로컬 머신 → Anthropic API 직결, 트랜스크립트는 dedup용 SHA-256 해시(12자)만 저장하고 원문은 디스크에 쓰지 않음
- **의존성 0 · 50KB** 풋프린트로 GitHub에서 코드 전량 감사 가능, hook 삭제만으로 언제든 비활성화

**의의**

AI 코딩 도구의 "세션 간 기억 상실" 문제를 Hook + 저비용 LLM 게이트로 직접 정의하고 해결해, 로컬에서 안전하게 동작하는 지식 축적 루프로 npm에 배포한 사례입니다.

---

### bumpist-code — 프론트엔드 표준 배포 CLI (Claude Code 스킬 허브)

Vue · React · Next.js 프론트엔드 공통 규칙과 Claude Code 스킬을 `npx` 한 줄로 프로젝트에 배선하는 오픈소스 CLI입니다. npm에 semver로 배포해 매번 같은 퀄리티로 작업하도록 표준을 고정하며, 실서비스 MVP([re-pin](https://github.com/parksubeom/re-pin)) 부트스트랩으로 Next.js 트랙까지 실전 검증했습니다.

<p align="center">
  <a href="https://www.npmjs.com/package/bumpist-code">
    <img src="https://img.shields.io/npm/v/bumpist-code?style=for-the-badge&label=npm&color=6d6afe&logo=npm&logoColor=white" alt="npm Version"/>
  </a>
  <a href="https://www.npmjs.com/package/bumpist-code">
    <img src="https://img.shields.io/npm/dt/bumpist-code?style=for-the-badge&label=Downloads&color=20C20E&logo=npm&logoColor=white" alt="npm Downloads"/>
  </a>
  <a href="https://github.com/parksubeom/bumpist-fe-guide">
    <img src="https://img.shields.io/badge/Repo-bumpist--fe--guide-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repository"/>
  </a>
</p>

> **▶ [npm에서 보기](https://www.npmjs.com/package/bumpist-code)** &nbsp;·&nbsp; 설치: `npx bumpist-code@latest init`

**해결한 문제**

프로젝트마다 폴더 구조·컴포넌트 작성법·테스트·커밋 컨벤션이 제각각이 되고, AI 코딩 도구에 매번 같은 맥락을 다시 알려줘야 했습니다. 프론트엔드 작업 표준(규칙)과 그 규칙을 실제 작업으로 옮겨 주는 Claude Code 스킬을 한 벌로 묶어, `npx` 한 줄로 어떤 프로젝트에나 복사·배선되게 만들었습니다.

**핵심 기능**
- `npx bumpist-code init` 한 줄로 규칙·스킬·문서를 프로젝트 `.claude/`에 복사하고 `CLAUDE.md`까지 자동 배선
- `package.json`으로 프레임워크(Vue/React/Next.js) 자동 감지 후 프레임워크별 규칙 선택 적용
- 작업 유형을 판별해 알맞은 규칙·스킬로 안내하는 14종 스킬(plan · create-slice · gen-api-types · write-test · prepare-pr 등)
- 뉴트럴·플랫·브랜드 컬러 1개·접근성(WCAG AA) 기반 디자인 기본선 + Feature-Sliced Design 아키텍처 내장

**기술적 의사결정**
- 서브모듈이 아닌 **복사 배포** 방식으로, 받은 시점의 버전이 프로젝트에 고정되고 원본 repo에 종속되지 않도록 설계
- npm **semver**(MAJOR: 깨지는 변경 / MINOR: 규칙·스킬 추가 / PATCH: 문구 수정)로 배포해 프로젝트별로 다른 표준 버전을 독립적으로 운용
- `.claude/.guide-version`에 받은 버전을 기록해 "이 프로젝트가 어느 표준 버전인지" 추적 가능
- 디자인 기본선은 자체 규칙으로 잡되, 심화 craft는 `impeccable` 스킬과 페어링하도록 경계를 명확히 분리

**의의**

반복되는 프론트엔드 셋업·컨벤션 정착 비용을 표준 패키지로 추출해, 사람이 읽어도 되고 Claude Code가 작업 전에 읽기도 하는 단일 출처로 만든 사례입니다.

---

### MathCanvas — 디지털 수학 교구 플랫폼 (2026 ~ , 코드넛)

비상교육과 협업하는 매쓰캔버스 플랫폼의 프론트엔드 개발입니다.

- Vue 3 Composition API + TypeScript 기반 선생님/학생 뷰어 및 활동 리포트 개발
- 컴포넌트 재사용으로 인한 stale state 버그를 lifecycle 가설 검증으로 추적하고 최소 변경(1줄)으로 차단
- shared/ui 레이어 변경 정책 정착(git blame → 사용처 분석 → API 호환 → 시각 검증)

---

### A11yGym — 웹 접근성 학습 플랫폼

- Monaco Editor와 axe-core 기반 실시간 접근성 검증 시스템 구축
- 3단계 비동기 방어 메커니즘으로 검사 안정성 99% 확보 및 5ms 이내 즉각적인 피드백 루프 구현

---

### AI-Native Portfolio

- AI 환각 제어 파이프라인(Context Injection)을 통한 고품질 FSD 아키텍처 구현
- ISR 전략 도입으로 SSR 대비 응답 속도 90% 개선(500ms → 50ms 미만)

---

### Hanghae-Plus Archiving

- 4-Layer Fallback 알고리즘 설계를 통한 데이터 유실률 0% 및 정합성 95% 달성
- 블랙박스 매칭 과정 가시화를 위한 자동 디버깅 리포트 생성 시스템 구축

---

## Values & Collaboration

- **Complexity to Simplicity**: 복잡한 레거시와 프로세스를 단순화합니다. 3일 소요되던 배포 과정을 실시간 자동화 시스템으로 개선한 경험이 있습니다.
- **Team Performance & DX**: 동료의 시간을 아끼는 것이 팀의 경쟁력이라 믿습니다. 개발자 친화적 가이드라인과 기술 교육으로 협업 병목을 해결합니다.
- **User-First & Data-Driven**: 웹 접근성 컨설팅 경험을 기반으로 표준을 준수하며, 데이터와 피드백으로 가설을 검증해 제품의 방향을 함께 고민합니다.
- **Root-Cause Driven**: 표면 증상에 대증적으로 대응하지 않고 데이터 검증으로 가설을 깨가며 진짜 원인을 찾습니다. 잘못된 가설에서 출발한 방어 코드 3종을 데이터 dump 하나로 기각시키고 단 1줄의 lifecycle 수정으로 해결한 경험이 있습니다.

---

## Work Experience

### (주)코드넛 | Frontend Developer (2026.03 - Present)
- **매쓰캔버스 플랫폼 개발**: 비상교육과 협업하는 디지털 수학 교구 플랫폼(매쓰캔버스)의 Vue 3 + TypeScript 기반 프론트엔드 개발
- **선생님/학생 뷰어 + 활동 리포트**: OX/선지/매쓰캔버스/돌림판/사다리 등 8종 슬라이드 컴포넌트와 학생 활동 리포트 시스템 구축
- **Lifecycle/Reactivity 디버깅**: BE 응답 schema 모호성으로 보였던 OX 퀴즈 썸네일 mismatch 버그를 데이터 dump 검증으로 컴포넌트 재사용 stale state 문제로 재정의하고 `watch + immediate` 1줄로 차단
- **Shared 레이어 회귀 차단**: 동일 sync 누수 패턴을 가진 Quiz 컴포넌트 5종(OX/PickText/SmartBank/LadderGame/SpinnerWheel) 12개 watcher에 readonly 가드 일괄 적용
- **디자인 시스템 매핑**: Figma 시안을 Tailwind 토큰으로 매핑해 arbitrary value 거의 없이 유지보수 가능한 반응형 UI 구축

### (주)에스앤씨랩 | Consultant & Developer (2024.07 - 2026.02)
- **협업 프로세스 혁신**: 소통 언어 표준화 및 가이드라인 배포로 평균 재진단 횟수 단축(2.5회 → 0~1회)
- **접근성 품질 인증(WA) 리딩**: 저축은행중앙회, 신협 등 대규모 프로젝트 심사 대응 및 1차 통과율 95% 달성
- **사내 지식 베이스 구축**: WCAG 2.2/3.0 최신 명세 분석 및 비개발 직군 대상 기술 교육 주도(질의 메일 40% 감소)

### 널리소프트(SSEM) | Frontend Developer (2024.03 - 2024.07)
- **배포 프로세스 자동화**: SVN API 기반 관제 대시보드 구축으로 배포 준비 시간 3일 단축 및 휴먼 에러 100% 차단
- **레거시 마이그레이션**: jQuery 레거시를 React로 현대화하며 중복 코드 제거(코드 라인 27% 절감)
- **전략적 리뉴얼**: 360px~2580px 대응 반응형 웹 구축 및 10개 이상의 공통 컴포넌트 설계로 유지보수성 확보

---

## Tech Stack

**Frameworks & Languages**

![TypeScript](https://img.shields.io/badge/typescript-%233178C6.svg?style=flat-square&logo=typescript&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23F7DF1E.svg?style=flat-square&logo=javascript&logoColor=black) ![React](https://img.shields.io/badge/react-%2361DAFB.svg?style=flat-square&logo=react&logoColor=black) ![Next.js](https://img.shields.io/badge/Next.js-black?style=flat-square&logo=next.js&logoColor=white) ![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=flat-square&logo=vuedotjs&logoColor=%234FC08D)

**State & Data**

![Zustand](https://img.shields.io/badge/Zustand-443E38?style=flat-square) ![Pinia](https://img.shields.io/badge/Pinia-FFD859?style=flat-square&logo=pinia&logoColor=black) ![TanStack Query](https://img.shields.io/badge/-Tanstack%20Query-FF4154?style=flat-square&logo=react-query&logoColor=white) ![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)

**Styling**

![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=flat-square&logo=tailwind-css&logoColor=white)

**Quality & Tools**

![Web Accessibility](https://img.shields.io/badge/Web_Accessibility-A11Y-blue?style=flat-square) ![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white) ![Figma](https://img.shields.io/badge/figma-%23F24E1E.svg?style=flat-square&logo=figma&logoColor=white)
