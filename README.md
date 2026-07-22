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

<details>
<summary><b>Claude Skills를 폴더 안 뒤지고 GUI에서 켜고 끄기 — Open VSX 배포</b></summary>

<br/>

**배경 · 문제**
- Claude Skills(SKILL.md 기반 작업별 지침 모음)는 유용하지만, 지금 어떤 스킬이 켜져 있는지 보려면 매번 `~/.claude/skills` 폴더를 직접 열어 확인해야 했다. 한눈에 보고 스위치처럼 켜고 끌 도구가 없어 직접 만들었다.

**접근**
- 워크스페이스·전역 스킬을 사이드 패널에 목록(Tree View)으로 보여주고, 파일을 직접 고치지 않고 클릭 한 번으로 켜고 끄게 했다.
- 스킬 설명(frontmatter의 name/description)을 목록에 마우스를 올리면 바로 보이게 하고, 파일이 추가·삭제되면 화면에 실시간 반영했다.
- 파일 변경 감지를 처음엔 기본 기능(`fs.watch`)으로 했는데 리눅스에서 하위 폴더를 못 잡고 저장을 놓치는 문제가 있어, 더 안정적인 라이브러리(chokidar)로 바꾸고 짧은 시간에 몰려 오는 변경은 하나로 묶었다(150ms 디바운스).
- 스킬 상태를 '프로젝트별'과 '전역'으로 나눠 저장해, 한 프로젝트 설정이 다른 프로젝트로 새지 않게 했다.
- 켜기/끄기를 각각 별도 명령으로 나눠, 빠르게 연타해도 상태가 꼬이지 않게 했다.
- 남이 만든 SKILL.md 내용을 신뢰하지 않도록 설정(`isTrusted = false`)해, 의도치 않은 명령 실행을 막았다.

**결과**
- 실제로 불편했던 문제를 직접 도구로 만들어 확장 마켓(Open VSX)에 publisher(`parksubeom.claude-skills-panel`)로 정식 배포했다.

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

</details>

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

<details>
<summary><b>AI가 지난 세션 교훈을 기억하게 — 대부분 무료로 동작</b></summary>

<br/>

**배경 · 문제**
- Claude Code는 대화 세션이 바뀌면 지난번에 배운 것·실수·의사결정을 기억하지 못해, 매번 같은 맥락을 다시 설명해야 했다("매일 새로 출근하는 알바생" 같은 문제).

**접근**
- 세션이 끝나면 자동으로 대화를 분석해 '배운 것'(`knowledge.md`)과 '실수·함정'(`gotchas.md`)을 파일로 쌓고, 11가지 종류로 분류했다.
- 대화의 한글 비율을 보고 한국어/영어를 자동으로 골라 기록하고, 결과는 그냥 텍스트(markdown)라 직접 고치거나 지울 수 있게 했다(지운 항목은 다음 세션에 다시 안 나옴).
- 비용을 줄이려 여러 단계로 걸렀다: 공짜 규칙으로 먼저 거르고 → 값싼 모델로 "기록할 가치가 있나?"만 한 번 묻고 → 중복 제거 순. 그 결과 세션의 약 90%가 비싼 분석 전에 걸러져, 비싼 호출이 약 1/10로 줄었다.
- 개인정보 보호를 위해 중간 서버 없이 내 컴퓨터에서 바로 API로 보내고, 대화 원문은 저장하지 않았다(중복 확인용 짧은 해시만 저장).
- 다른 라이브러리 없이 50KB로 만들어 코드를 통째로 확인할 수 있고, 설정만 지우면 언제든 끌 수 있다.

**결과**
- 대부분 세션은 거의 0원, 실제 분석까지 간 세션만 약 0.1달러 수준으로 비용을 눌렀다. npm에 배포.

</details>

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

<details>
<summary><b>프론트엔드 작업 규칙을 명령어 한 줄로 새 프로젝트에 세팅</b></summary>

<br/>

**배경 · 문제**
- 프로젝트마다 폴더 구조·컴포넌트 작성법·테스트·커밋 방식이 제각각이 되고, AI 코딩 도구에도 매번 같은 규칙을 다시 알려줘야 했다. 그래서 작업 규칙과 그 규칙대로 일해 주는 Claude Code 스킬을 한 묶음으로 만들어, 명령어 한 줄로 어떤 프로젝트에나 깔리게 했다.

**접근**
- `npx bumpist-code init` 한 줄이면 규칙·스킬·문서가 프로젝트 `.claude/`에 복사되고 `CLAUDE.md`까지 자동 연결된다.
- `package.json`을 보고 어떤 프레임워크(Vue/React/Next.js)인지 자동으로 알아내 맞는 규칙을 고른다.
- 작업 종류에 맞는 14개 스킬(계획 세우기·기능 추가·API 타입 생성·테스트 작성·PR 준비 등)을 제공한다.
- 접근성 기준(WCAG AA)과 폴더 구조 설계 방식(Feature-Sliced Design)을 기본으로 넣었다.
- 원본에 계속 연결되는 방식이 아니라 '복사해서 넣는' 방식이라, 받은 시점의 버전이 그대로 고정된다.
- 버전 규칙(semver)으로 배포해 프로젝트마다 다른 버전을 따로 쓸 수 있고, 어떤 버전을 받았는지 기록해 둔다.

**결과**
- npm에 배포하고, 실제 서비스 MVP([re-pin](https://github.com/parksubeom/re-pin))을 이걸로 시작해 Next.js 트랙까지 검증했다.

</details>

---

### MathCanvas — 웹 기반 수학 교육 저작·발표 도구 (프론트엔드)

초·중등 수학 수업용 웹 도구입니다. 교사가 3D 입체·저울·수직선 같은 수학 교구를 화면에 배치하고, 슬라이드로 엮어 발표까지 하며, 발표자 화면이 학생 화면에 실시간으로 미러링됩니다. Vue 3 · TypeScript · Pinia로 만들고 3D는 Three.js(WebGL)로 그리며, 코드는 Feature-Sliced Design으로 구조화했습니다.

성능·안정성 문제를 만날 때마다 어떤 선택지에서 무엇을·왜 골랐고 결과가 어땠는지를 기록했습니다. 수치는 모두 계측으로 검증했습니다.

<details>
<summary><b>학생·교사·발표자 화면의 렌더링 경로 통합 + 학생 풀이 과정 재생 엔진</b></summary>

<br/>

학생·교사·발표자가 동일한 인터랙티브 캔버스를 공유하되, 각 역할은 서로 다른 실행 컨텍스트(메인 앱 vs CDN 임베드)에서 동작한다.

**배경 · 문제**
- 학생·발표자 화면은 CDN 번들로 shadow DOM 안에 임베드되는데, 교사 뷰어만 메인 앱에서 캔버스를 직접 렌더했다. 하나의 캔버스가 서로 다른 두 렌더링 경로를 타면서 교구 동작·좌표계·재생 결과가 화면마다 어긋났다.
- 학생 풀이를 교사가 다시 볼 때 재생이 중간 과정 없이 최종 상태로 즉시 스냅되어, 풀이 과정을 따라 보며 지도하는 핵심 시나리오가 성립하지 못했다.

**접근**
- **렌더링 경로 통일** — 교사 뷰어를 메인 앱 직접 렌더에서 CDN 임베드로 이관해 세 역할을 같은 렌더링 파이프라인으로 모았다. 한 번에 전환하는 리스크를 줄이려 feature flag로 감싸 6단계로 점진 적용했다.
- **크로스번들 통신 브릿지** — CDN 번들은 독립된 Pinia 스토어와 shadow DOM을 써서 메인 앱과 상태를 직접 공유할 수 없다. window 커스텀 이벤트로 두 컨텍스트를 연결하고, 리스너 등록 시점에 올바른 Pinia 인스턴스를 캡처해 잘못된 스토어에 상태가 기록되는 버그를 차단했다.
- **히스토리 재생 엔진** — 학생의 조작을 스트림으로 기록해 두고 교사 뷰어에서 재구성해 재생했다. 일반 객체는 이동 경로 구간을 보간(tween)해 부드럽게, 3D 교구는 카메라 상태를 보간해 궤적을 살렸다.
- **재생 충실도 개선** — 한 프레임에 몰아 그려 스냅되던 재생을 조작 타임스탬프에 비례해 배속(0.5~2배) 구간에 분산 렌더하도록 바꿨다. 최종 상태로 갔다가 시작점으로 되돌아오던 아티팩트를 제거하고, 히스토리에 누락돼 재생 시 사라지던 교구 16종의 조작도 기록되게 했다.

**결과**
- 학생·교사·발표자 세 역할의 렌더링 경로를 하나로 통합해 재생 결과·좌표 일관성을 확보.
- 재생을 정적 스냅에서 배속 연동 트레이스 애니메이션으로 전환(주사위 재생 약 11s → 4.9s @0.5×).
- 회귀 방지 테스트 20개를 함께 작성, 64개 파일·3,700여 줄 변경을 회귀 없이 반영.

</details>

<details>
<summary><b>성능·안정성 개선 6건</b> — 슬라이드 9배 · WebGL · 발표 백지 해결 · 계측 기반 원인 추적</summary>

<br/>

**① 슬라이드 이동 성능 — 2.8초 → 0.3초 (약 9배)**
- 상황: 슬라이드를 넘길 때마다 현재 화면을 통째로 이미지로 저장하느라 전환이 ~2.8초 블로킹
- 어떻게: 화면 전체를 한 번에 저장하던 방식을 버리고 화면 구성요소(수식·필기·3D)를 따로 합성 + "실제로 편집했을 때만" 저장하도록 변경
- 왜: 병목이 화질(해상도)이 아니라 "화면 전환 직전에 저장이 끝나길 기다리는" 구조였기 때문 — 저장을 전환과 분리하면 대기 자체가 사라짐
- 효과: 전환 ~2.8초 → ~0.3초, 보기만 할 땐 기존 썸네일 유지

**② WebGL 렌더 부하 — 51 → 13fps (약 4배)**
- 상황: 3D 교구가 화면이 그대로여도 매 순간 다시 그려져, 여러 개가 겹치면 프레임 드롭
- 어떻게: "상태가 바뀔 때만 다시 그리기"로 전환, 카메라를 움직이는 동안만 잠깐 연속 렌더 후 정지
- 왜: 아무것도 안 바뀐 순간에도 계속 그리는 게 낭비 — 유휴 시 0프레임이면 성능 저하 없이 필요할 때만 렌더
- 효과: 51 → 13fps, 유휴 상태 오버헤드 0

**③ 발표 중 학생 화면이 하얗게 꺼짐 — 임시책 대신 근본 해결**
- 상황: 브라우저가 동시에 띄우는 3D 화면 수 한계(16개)를 발표자·학생 두 창이 나눠 쓰다 교구 9종×2창=18개로 초과 → 학생 화면 꺼짐
- 어떻게: 응답 대기시간을 늘려 버티는 임시책 대신, 여러 교구가 3D 화면 하나를 공유하도록 근본 수정(창당 9개 → 1개, 즉시 되돌릴 스위치 포함)
- 왜: 대기시간을 늘려도 16개 한계는 그대로라 결국 재발 — 한도 자체를 넘지 않아야 근본 해결
- 효과: 3D 화면 18개 → 2개, 백지·강제종료 해소

**④ 3D 교구 소멸 버그 — 일괄 수정 대신 정밀 수정**
- 상황: 한 버그를 잡으려 공통 로직에 일괄 수정(중복 제거)을 넣으려던 상황
- 어떻게: 일괄 수정을 폐기하고 문제가 확인된 특정 경로만 정밀 수정
- 왜: 배포 전 여러 각도로 검증하니 그 일괄 수정이 드래그·회전·되돌리기 등 190여 곳에서 교구를 전부 사라지게 함 — 한 증상 잡으려다 더 큰 붕괴를 부르면 비용 > 이득
- 효과: 광범위한 붕괴를 배포 전 차단하고 원래 증상만 안전하게 해결

**⑤ 렌더 실패 — 위험한 근본 수정 대신 안전장치 먼저**
- 상황: 특정 상황에서 3D 교구가 아무 오류 없이 화면에서 사라짐(그릴 대상이 비어 조용히 실패)
- 어떻게: 원인(중복 초기화)을 통째로 고치는 대신 "비어 버린 화면을 그 자리에서 되살리는" 작은 가드를 먼저 적용, 근본 수정은 별도 작업으로 분리
- 왜: 근본 수정은 초기화·되돌리기·슬라이드 전환 전반을 건드려 검증 범위가 넓고 위험 — 가드는 화면 복구 지점만 건드려 위험이 국소적
- 효과: 증상 즉시 해소 + 전체 테스트 무회귀 통과, 근본은 위험을 분리해 관리

**⑥ 판단 근거 — 눈대중 대신 계측**
- 상황: 원격 화면은 전송 지연 탓에 성능 체감이 실제와 왜곡됨
- 어떻게: 처리 시간·프레임 주기·3D 화면 사용량을 코드로 직접 계측하고 켜고 끄며 A/B로 비교
- 왜: 체감이 아니라 숫자로 봐야 원인·효과가 확정됨 — 처음 세운 원인 가설(누적 문제)이 계측으로 반증되며 진짜 원인(두 창의 GPU 공유)을 특정
- 효과: 특정 조작 시 화면 멈춤 16회 → 1회를 수치로 확인 후 배포

</details>

**일하는 방식**
- 선택지·위험도를 표로 정리해 기획자·PM에게 쉬운 말로 먼저 제시 → 논의 라운드 단축
- 문제를 고칠 때마다 방어 코드와 재발 방지 테스트를 짝으로 남기고(정적·런타임·통합 3층), 유닛·통합 테스트 800개 이상으로 회귀 상시 차단
- 가설이 측정으로 틀리면 그 가설 기반 수정·테스트를 함께 되돌리고 원인을 재조사(지적 정직성)

**의의**

문제를 스스로 정의하고(계측), 근거로 설득하고(선택지 비교표), 재발까지 막는(테스트) 사이클을 상용 서비스에서 반복하며, 성능·구조 문제를 판단 근거와 함께 해결한 사례입니다.

---

### Hanghae-Plus Archiving — 과제 제출 이력 아카이빙 서비스

항해플러스 수강생의 과제 제출 이력이 LMS에서 휘발되는 문제를 해결한 아카이빙 서비스. GitHub API로 제출 이력을 자동 수집하고, 결함 허용(Fault Tolerant) 매칭으로 데이터 유실률 0%를 달성했다.

`개인 프로젝트 · Full Stack · 2025.12–2026.01` &nbsp;·&nbsp; `Node.js · NestJS · GitHub API · React · Tailwind CSS · Supabase`

<details>
<summary><b>LMS에서 휘발되던 과제 제출 이력 아카이빙 — 결함 허용 매칭으로 유실률 0%</b></summary>

<br/>

**배경 · 문제**
- 수강생이 제출한 과제(PR) 링크가 Re-open·리포지토리 포맷 변경·계정 ID 불일치 등으로 자주 바뀌어, LMS에서 제출 이력이 누락·휘발됐다. 단순 문자열 매칭으로는 정합성을 보장할 수 없어, GitHub API 기반 자동 수집 파이프라인과 실패에 강한 매칭 로직이 필요했다.

**접근**
- **4-Layer Fallback 매칭 알고리즘 (핵심)** — 한 단계가 실패하면 다음 단계로 순차 복구하는 결함 허용 알고리즘을 직접 설계했다: ① URL 표준화(www 제거·트레일링 슬래시 통일) ② 실명과 GitHub ID가 다른 약 5% 케이스를 매핑 테이블로 강제 연결 ③ 과제명(Chapter) 키워드로 유저의 이벤트 히스토리를 역추적해 오기입 링크 복구 ④ Fork·원본 리포지토리의 PR 번호를 대조해 유실분 추적.
- **관측 가능성(Observability)** — 매칭 로직이 복잡해질수록 실패 원인 파악이 어려워지는(블랙박스) 문제를, 매칭 실행마다 성공/실패 원인과 매칭 경로를 분석한 디버깅 리포트(`matching-debug.md`)를 자동 생성해 해결. 원인 파악을 수십 분 → 즉시로 단축.
- **게이미피케이션·인터랙티브 UI** — 단순 점수제를 폐지하고 완료율과 베스트 프랙티스(BP)를 복합 평가하는 6단계 등급 시스템(`ranking.utils.ts`)으로 재설계. 프로필 카드에 CSS 3D Transform(perspective·rotateY) 기반 flip 애니메이션을 적용하고 `will-change`로 렌더링을 최적화, 커스텀 cubic-bezier 이징으로 모션을 다듬음. 등급에 따라 그라데이션·글래스모피즘·SVG 뱃지가 자동으로 바뀌는 동적 스타일링 시스템 구축.
- **SSR Hydration Mismatch 해결** — 배포 서버(UTC)와 클라이언트(KST)의 타임존 차이로 날짜가 달라져 hydration 에러가 발생. 런타임 진입점에서 타임존을 서울로 고정하고, UTC 기준 포맷팅 + 클라이언트 전용 훅 초기값 통일로 서버/클라이언트 렌더 결과를 일치시킴.

**결과**
- 매칭 정확도 초기 실패율 40% → 95% 이상, 단순 URL 매칭으로 못 찾던 40% 이상의 누락 데이터 복구.
- 수동 개입이 필요한 케이스를 전체의 5% 미만으로 축소, 데이터 유실률 0% 달성.

</details>

---

## Values & Collaboration

- **Complexity to Simplicity**: 복잡한 레거시와 프로세스를 단순화합니다. 3일 소요되던 배포 과정을 실시간 자동화 시스템으로 개선한 경험이 있습니다.
- **Team Performance & DX**: 동료의 시간을 아끼는 것이 팀의 경쟁력이라 믿습니다. 개발자 친화적 가이드라인과 기술 교육으로 협업 병목을 해결합니다.
- **User-First & Data-Driven**: 웹 접근성 컨설팅 경험을 기반으로 표준을 준수하며, 데이터와 피드백으로 가설을 검증해 제품의 방향을 함께 고민합니다.
- **Root-Cause Driven**: 표면 증상에 대증적으로 대응하지 않고 데이터 검증으로 가설을 깨가며 진짜 원인을 찾습니다. 잘못된 가설에서 출발한 방어 코드 3종을 데이터 dump 하나로 기각시키고 단 1줄의 lifecycle 수정으로 해결한 경험이 있습니다.

---

## Work Experience

### (주)코드넛 | Frontend Developer (2026.03 - Present)
- **매쓰캔버스 플랫폼 개발**: 웹 수학 교육 저작·발표 도구를 Vue 3 · TypeScript · Pinia · Three.js(WebGL) + Feature-Sliced Design으로 개발 — 교구 캔버스·8종 슬라이드·학생 활동 리포트·발표자–학생 실시간 미러링
- **슬라이드 전환 9배 개선**: 화면 전환마다 통째로 이미지를 저장하던 병목을, 저장을 전환과 분리하고 편집 시에만 저장하도록 재설계해 ~2.8초 → ~0.3초
- **3D 렌더 성능·안정화**: 매 순간 다시 그리던 3D를 "바뀔 때만 그리기"로 전환(13→51fps, 유휴 부하 0), 발표 시 브라우저 3D 화면 한도 초과로 학생 화면이 꺼지던 문제를 렌더러 공유(창당 9→1개)로 해소
- **계측 기반 원인 추적**: 처리 시간·프레임 주기·3D 화면 사용량을 직접 측정하고 A/B로 비교해, 체감이 아닌 수치로 원인을 특정(특정 조작 시 화면 멈춤 16회 → 1회)
- **회귀 차단**: 컴포넌트 재사용으로 생긴 화면 갱신 버그를 데이터로 재정의해 1줄로 차단하고, 같은 패턴을 가진 5개 컴포넌트에 가드를 일괄 적용; 정적·런타임·통합 3층 테스트 800개 이상 상시 운영
- **디자인 시스템 매핑**: Figma 시안을 Tailwind 토큰으로 매핑해 유지보수 쉬운 반응형 UI 구축

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
