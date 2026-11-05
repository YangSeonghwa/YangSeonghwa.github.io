# 🌸 Beflower의 수업 연구실 (yangseonghwa.github.io)

중학교 과학 교사 **Beflower**가 AI와 함께 바이브 코딩으로 만드는 **학년별 과학 웹 시뮬레이션**과 **프로그램(바이브 코딩) 수업 자료** 모음입니다.
사이트: https://yangseonghwa.github.io/

이 저장소는 **GitHub Pages 전용 정적 웹사이트**입니다. 웹페이지(HTML, CSS, JavaScript, 이미지)만 두고 실행 파일(exe)은 만들지 않습니다.

## 구조

```
index.html            # 메인 페이지 (과학 시뮬레이션 + 프로그램 수업 + 미니게임)
GUIDELINES.md         # [필수] 공통 디자인 시스템(Beflower Design System) 및 제작 지침서
assets/css/beflower.css # 전 페이지 공통 디자인 시스템 스타일시트
templates/            # 새 시뮬레이션·수업·활동지·게임 표준 HTML 템플릿 4종
sims.json             # 과학 시뮬레이션 목록
lessons.json          # 프로그램 수업 목록
games.json            # 미니게임 목록
grade1/ grade2/ grade3/   # 학년별 과학 시뮬레이션
programming/          # 프로그램 수업 자료 (수업마다 폴더 하나)
games/                # 교육용 미니게임
images/               # 이미지
```

## 디자인 시스템 및 새 페이지 제작 지침 (`GUIDELINES.md`)

모든 페이지(과학 실험실, 코딩·AI 발표 슬라이드, 활동지, 미니게임)는 **`assets/css/beflower.css` 공통 디자인 시스템**을 통해 일관된 브랜드 헤더(`.bf-topbar`), 네비게이션(`🏠 홈으로`), 푸터(`.bf-footer`), 오프라인 안전 시스템 폰트 스택, 컬러 팔레트(Light / Dark Lab 테마)를 공유합니다.

새 페이지를 만들 때는 **`GUIDELINES.md`**를 먼저 읽고 **`templates/`** 폴더의 표준 템플릿(`simulation-template.html`, `lesson-slides-template.html`, `worksheet-template.html`, `game-template.html`)을 복사해 시작하세요.

## 새 과학 시뮬레이션 추가

1. `gradeN/주제명/index.html` 위치에 시뮬레이션을 둡니다.
2. `sims.json`에 한 줄을 추가합니다.

```json
{ "grade": 1, "area": "물리", "title": "힘의 합성", "desc": "두 힘의 합력 관찰", "url": "grade1/force/index.html" }
```

## 새 프로그램 수업 추가

1. `programming/수업이름/index.html` 위치에 수업 자료(발표 페이지 등)를 둡니다.
2. `lessons.json`에 한 줄을 추가합니다.

```json
{ "type": "발표 자료", "level": "공통", "title": "수업 제목", "desc": "한 줄 설명", "url": "programming/수업이름/index.html" }
```

## 발표 페이지 사용법

`programming/chatgpt-github-vibe/` 페이지: 방향키·스페이스·터치 스와이프로 넘기고, `F` 전체화면, `N` 교사 메모, 인쇄하면 모든 슬라이드가 출력됩니다.

## 배포

Settings → Pages → Branch `main` / root. `main`에 푸시하면 곧바로 공개됩니다. 미리보기는 `python -m http.server` 로 여세요 (`index.html`을 파일로 직접 열면 JSON을 불러오지 못할 수 있습니다).
