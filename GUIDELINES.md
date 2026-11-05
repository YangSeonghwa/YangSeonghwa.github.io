# 🌸 Beflower의 과학 시뮬레이션 랩 — 디자인 및 개발 지침서 (GUIDELINES.md)

이 문서는 **Beflower의 과학 시뮬레이션 랩 (`yangseonghwa.github.io`)** 프로젝트에 새로운 웹 페이지(과학 시뮬레이션, 수업 슬라이드, 탐구 활동지, 교육용 게임 등)를 추가하거나 기존 페이지를 수정할 때 **어떤 AI 에이전트나 개발자가 작업하더라도 일관된 브랜드 경험과 UI/UX를 유지**할 수 있도록 정의한 공식 디자인 시스템 및 개발 표준입니다.

---

## 1. 핵심 아키텍처 원칙

1. **공통 스타일시트(`assets/css/beflower.css`) 필수 로드**
   - 모든 HTML 페이지는 `<head>` 내부에서 `assets/css/beflower.css`를 상대 경로로 반드시 불러와야 합니다.
   - 루트(`/`): `assets/css/beflower.css`
   - 1단계 하위(`games/` 등): `../assets/css/beflower.css`
   - 2단계 하위(`grade1/charles-law/`, `programming/chatgpt-github-vibe/` 등): `../../assets/css/beflower.css`
2. **외부 빌드 도구 없는 순수 정적 웹(Vanilla HTML/CSS/JS)**
   - GitHub Pages에서 즉시 동작하도록 별도의 번들러 없이 **단일 HTML + 공통 CSS(`beflower.css`)** 구조를 유지합니다.
   - 모든 내부 링크와 리소스 참조는 **상대 경로**(`../../index.html` 등)를 사용합니다.
3. **자가 완결성 및 반응형/인쇄 호환성**
   - 교실 전자칠판(16:9 와이드), 태블릿/크롬북, 스마트폰(360px 이상)에서 가로 스크롤 깨짐 없이 동작해야 합니다.
   - 슬라이드 및 활동지 페이지는 `@media print`를 통해 A4 인쇄/PDF 저장 시 배경 장식과 상·하단 고정 바가 숨겨지고 깔끔하게 출력되어야 합니다.

---

## 2. 디자인 토큰 (Design Tokens)

`assets/css/beflower.css`의 `:root`에 정의된 CSS 변수를 사용합니다. 페이지별 `<style>`에서도 하드코딩된 색상 대신 아래 변수를 우선 참조하세요.

### 2.1 컬러 팔레트 (Light Mode 기본 & Dark Mode 테마)

| 구분 | CSS 변수 | 기본값 (Light) | 다크 테마 (`.bf-theme-dark`) | 용도 |
| :--- | :--- | :--- | :--- | :--- |
| **브랜드 메인 (Teal)** | `--bf-main` | `#1f8a70` | `#2bb393` | 주요 버튼, 활성 탭, 강조 포인트 |
| **브랜드 메인 다크** | `--bf-main-dark` | `#146350` | — | 버튼 호버, 진한 포인트 |
| **브랜드 소프트 배경** | `--bf-main-soft` | `#e6f5f0` | `rgba(43,179,147,0.18)` | 뱃지/콜아웃 배경, 선택 영역 |
| **브랜드 네이비** | `--bf-navy` | `#0f2a44` | — | 히어로 배너, 딥 다크 헤더 그라데이션 |
| **브랜드 핑크 (Blossom)** | `--bf-pink` | `#f08fb0` | — | 벚꽃 로고 그라데이션, 보조 포인트 |
| **페이지 배경** | `--bf-bg` | `#f6f8fb` | `#070b19` | 전체 `body` 기본 배경 |
| **카드 표면** | `--bf-surface` | `#ffffff` | `#10172e` | 카드, 패널, 슬라이드 컨테이너 배경 |
| **보조 표면** | `--bf-surface-soft` | `#eef3f9` | `#182344` | 입력창, 코드 블록, 비활성 탭 배경 |
| **본문 텍스트** | `--bf-ink` | `#16202a` | `#f1f5f9` | 제목 및 기본 본문 텍스트 |
| **보조 텍스트** | `--bf-sub` | `#526171` | `#94a3b8` | 부제목, 설명, 캡션, 메타 정보 |
| **보더/구분선** | `--bf-line` | `#dde5ef` | `rgba(148,163,184,0.24)` | 카드 테두리, 구분선 |

### 2.2 과목 및 카테고리 액센트 컬러

| 카테고리 | 메인 컬러 변수 | 소프트 배경 변수 | 뱃지 클래스 |
| :--- | :--- | :--- | :--- |
| **화학 / 입자 (Chemistry)** | `--bf-chem` (`#f97316`) | `--bf-chem-soft` (`#fff3e6`) | `.bf-badge.화학`, `.bf-badge.chem` |
| **물리 / 전기·자기 (Physics)** | `--bf-phys` (`#2563eb`) | `--bf-phys-soft` (`#eaf1ff`) | `.bf-badge.물리`, `.bf-badge.physics` |
| **지구과학 / 천문 (Astronomy)** | `--bf-astro` (`#6d28d9`) | `--bf-astro-soft` (`#f2ecff`) | `.bf-badge.지구과학`, `.bf-badge.astro` |
| **생명과학 (Biology)** | `--bf-bio` (`#16a34a`) | `--bf-bio-soft` (`#e8f8ee`) | `.bf-badge.생물`, `.bf-badge.bio` |
| **프로그래밍 / AI (Coding)** | `--bf-code` (`#0d9488`) | `--bf-code-soft` (`#e6faf6`) | `.bf-badge.프로그래밍`, `.bf-badge.coding` |
| **게임 / 아케이드 (Games)** | `--bf-game` (`#e11d48`) | `--bf-game-soft` (`#ffe9ef`) | `.bf-badge.게임`, `.bf-badge.game` |

### 2.3 타이포그래피 & 레이아웃 토큰

- **기본 폰트 (`--bf-font-sans`)**: `'Pretendard', 'Noto Sans KR', -apple-system, BlinkMacSystemFont, 'Malgun Gothic', sans-serif`
- **코드/수식 폰트 (`--bf-font-mono`)**: `'JetBrains Mono', 'Fira Code', 'Consolas', monospace`
- **최대 컨테이너 폭 (`--bf-max-width`)**: `1180px`
- **상단바 높이 (`--bf-topbar-h`)**: `60px`
- **라운딩**: `--bf-radius-xl` (`24px`), `--bf-radius-lg` (`18px`), `--bf-radius-md` (`12px`), `--bf-radius-sm` (`8px`), `--bf-radius-pill` (`999px`)

---

## 3. 공통 레이아웃 컴포넌트 규격

모든 페이지는 **상단 글로벌 네비게이션 바(`.bf-topbar`)**를 포함해야 하며, 스크롤형 페이지는 **하단 공통 푸터(`.bf-footer`)**를, 전체화면 슬라이드 덱은 **하단 슬라이드 컨트롤 바(`.bf-slide-bar`)**를 포함합니다.

### 3.1 상단 글로벌 네비게이션 바 (`.bf-topbar`)

`index.html`의 카테고리 섹션 앵커(`#sims`, `#coding`, `#games`)와 연결되는 4개의 표준 메뉴(`🏠 홈`, `🧪 시뮬레이션`, `💻 프로그램 수업`, `🎮 게임`)를 제공합니다. 현재 페이지의 성격에 맞는 메뉴 항목에 `class="active"`를 부여하세요.

```html
<!-- 기본 스크롤 페이지: class="bf-topbar" -->
<!-- 전체화면 슬라이드 페이지(상단 고정): class="bf-topbar bf-topbar-fixed" -->
<!-- 다크 테마 페이지: class="bf-topbar bf-topbar-dark" -->
<header class="bf-topbar">
  <div class="bf-topbar-inner">
    <a class="bf-brand" href="../../index.html">
      <span class="bf-brand-logo" aria-hidden="true">🌸</span>
      <span class="bf-brand-text">
        <span class="bf-brand-title">Beflower의 과학 시뮬레이션 랩</span>
        <span class="bf-brand-sub">중1 과학 · 기체의 성질 (샤를 법칙)</span>
      </span>
    </a>

    <nav class="bf-nav" aria-label="주요 메뉴">
      <a href="../../index.html">🏠 홈</a>
      <a class="active" href="../../index.html#sims">🧪 시뮬레이션</a>
      <a href="../../index.html#coding">💻 프로그램 수업</a>
      <a href="../../index.html#games">🎮 게임</a>
    </nav>

    <!-- 선택 사항: 슬라이드 점프 셀렉트 박스, 인쇄 버튼, 교사용 해설 토글 등 -->
    <div class="bf-topbar-actions">
      <!-- 페이지별 보조 액션 버튼 배치 -->
    </div>
  </div>
</header>
```

### 3.2 페이지 타이틀 배너 (`.bf-page-header`)

스크롤형 시뮬레이션, 활동지, 게임 페이지 상단에 배치하는 표준 헤더 카드입니다.

```html
<section class="bf-page-header">
  <div class="bf-badge-row">
    <span class="bf-badge 물리">⚡ 중2 과학 · 물리</span>
    <span class="bf-badge">인터랙티브 실험실</span>
  </div>
  <h1 class="bf-page-title">페이지 메인 제목</h1>
  <p class="bf-page-desc">학습 목표 및 페이지 핵심 설명을 1~2문장으로 작성합니다.</p>
</section>
```

### 3.3 하단 공통 푸터 (`.bf-footer`)

스크롤형 페이지(`index.html`, 시뮬레이션, 활동지, 게임 등)의 `</body>` 직전에 배치합니다.

```html
<footer class="bf-footer">
  <div class="bf-footer-inner">
    <div class="bf-footer-brand">
      <span>🌸</span>
      <span>Beflower의 과학 시뮬레이션 랩 · YangSeonghwa.github.io</span>
    </div>
    <div class="bf-footer-links">
      <a href="../../index.html">홈으로</a>
      <a href="../../index.html#sims">과학 시뮬레이션</a>
      <a href="../../index.html#coding">프로그램 수업</a>
      <a href="../../index.html#games">교육용 게임</a>
      <a href="https://github.com/YangSeonghwa/YangSeonghwa.github.io" target="_blank" rel="noopener">GitHub</a>
    </div>
  </div>
</footer>
```

### 3.4 슬라이드 덱 전용 하단 컨트롤 바 (`.bf-slide-bar`)

전체화면 슬라이드형 수업 자료(`lesson-slides-template.html`)에서는 하단 고정 컨트롤 바(`.bf-slide-bar`)를 사용하며, 키보드 방향키(`←`, `→`, `Space`), `N`(교사용 해설 토글), `F`(전체화면) 단축키를 지원합니다.

---

## 4. 페이지 유형별 표준 템플릿 (`templates/`)

새 페이지를 만들 때는 아래 4가지 표준 템플릿 중 목적에 맞는 파일을 복사하여 시작하세요.

| 페이지 유형 | 템플릿 경로 | 주요 용도 및 특징 |
| :--- | :--- | :--- |
| **과학 시뮬레이션** | `templates/simulation-template.html` | 좌측 시각화 캔버스 + 우측 조작 패널/측정 지표(2단 반응형 그리드) + 하단 원리/퀴즈 탭 |
| **수업용 슬라이드 덱** | `templates/lesson-slides-template.html` | 전자칠판 수업용 16:9 슬라이드 쇼, 상단 고정 헤더(`.bf-topbar-fixed`), 하단 진행률 바(`.bf-slide-bar`), 교사용 노트(`N`키) |
| **학생용 탐구 활동지** | `templates/worksheet-template.html` | 학번/이름 기입란, 탐구 데이터 표, 서술형 문항, 자동저장(`localStorage`) 및 A4 인쇄/PDF 최적화 |
| **교육용 아케이드/게임** | `templates/game-template.html` | 점수판/타이머 HUD, 게임 보드, 난이도 선택 및 결과 모달 |

---

## 5. 새 페이지 추가 및 배포 체크리스트

새로운 페이지를 생성한 뒤 커밋하기 전에 반드시 다음 항목을 확인하세요.

1. **디렉터리 위치 규칙**
   - 중1 과학: `grade1/<topic-slug>/index.html`
   - 중2 과학: `grade2/<topic-slug>/index.html`
   - 중3 과학: `grade3/<topic-slug>/index.html`
   - 프로그래밍/AI 수업: `programming/<topic-slug>/index.html` (부속 활동지는 `worksheet.html` 등)
   - 게임: `games/<game-slug>/index.html`
2. **디자인 시스템 적용 확인**
   - `<head>`에 `<link rel="stylesheet" href=".../assets/css/beflower.css">`가 정확한 상대 경로로 포함되었는가?
   - Pretendard 웹폰트 CDN 링크가 포함되었는가?
   - 상단 `.bf-topbar`의 브랜드 링크와 4개 메뉴(`홈`, `시뮬레이션`, `프로그램 수업`, `게임`)의 상대 경로가 정확한가?
3. **메인 포털(`index.html`) 및 문서 업데이트**
   - `index.html`의 해당 카테고리 그리드에 새 페이지로 이동하는 `.sim-card` 카드를 추가했는가?
   - `PROJECT.md` 및 `README.md`의 콘텐츠 목록에 새 페이지 정보를 반영했는가?
4. **자동 검증 스크립트 실행**
   - 루트 워크스페이스에서 아래 명령을 실행하여 깨진 링크나 누락된 자산이 없는지 검증합니다:
     ```bash
     python3 scripts/pages_tool.py check
     python3 scripts/run_tests.py yangseonghwa.github.io
     ```
