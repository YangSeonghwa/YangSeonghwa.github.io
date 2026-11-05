# yangseonghwa.github.io

## 목적
Beflower(중학교 과학 교사)의 GitHub Pages 홈페이지. 학년별 과학 시뮬레이션과 프로그램(바이브 코딩) 수업 자료를 정적 웹페이지로 공개한다. **웹페이지만 있는 Pages 전용 프로젝트**이며 Windows exe는 만들지 않는다.

## 현재 상태
- 진행도: 운영 중 (https://yangseonghwa.github.io/)
- 마지막 갱신: 2026-04-20 by antigravity
- 지금 되는 것:
  - **Beflower 공통 디자인 시스템(`assets/css/beflower.css`) 및 제작 지침서(`GUIDELINES.md`), 표준 템플릿 4종(`templates/`)** 구축 및 전 페이지(8개 기존 HTML) 디자인/네비게이션/폰트/컬러 팔레트 통일 완료
  - 과학 시뮬레이션 목록(sims.json, 중1·중2), 프로그램 수업 목록(lessons.json), 프로그램 수업 발표 페이지(15장), 학생용 인쇄 활동지(worksheet.html), 중학교 2학년 「별의 밝기와 등급」 발표 자료 및 역제곱 법칙 시뮬레이션(`grade2/star-brightness/`), 중학교 2학년 「천체의 색깔과 별까지의 거리 판별」 발표 자료 및 인터랙티브 시뮬레이션(`grade2/star-color-distance/`), 게임 탭(games.json, 수박 터뜨리기)
- 아직 안 되는 것: 중학교 3학년 시뮬레이션, 바이브 코딩 수업의 실제 학생별 배포 실습 검증
- 저장소: 이 프로젝트는 전용 GitHub 저장소(`YangSeonghwa/YangSeonghwa.github.io`, **public**)를 가진다 (D-007). 서버의 `projects/yangseonghwa.github.io/`가 그 저장소의 작업 폴더이다. 공개 저장소이고 푸시하면 Pages가 곧바로 공개하므로 개인정보·비밀·학생 정보를 절대 넣지 않는다.

## 실행 방법
```
설치: 필요 없음 (순수 HTML/CSS/JavaScript)
무결성 검증: python3 scripts/pages_tool.py check   (또는 python3 scripts/run_tests.py yangseonghwa.github.io)
새 항목 스캐폴딩:
  python3 scripts/pages_tool.py add-sim --grade 2 --area 물리 --slug my-sim --title "제목" --desc "설명"
  python3 scripts/pages_tool.py add-lesson --slug my-lesson --title "제목" --desc "설명"
  python3 scripts/pages_tool.py add-game --slug my-game --icon "🎮" --title "제목" --desc "설명"
미리보기: python3 -m http.server   (저장소 폴더에서 실행하고 브라우저에서 localhost:8000 열기)
푸시:   git -C projects/yangseonghwa.github.io push
```
- 배포: `main` 브랜치 최상위 폴더를 GitHub Pages가 그대로 공개한다 (Settings → Pages → Deploy from a branch). 별도 빌드 단계가 없다.
- Windows exe·CI 워크플로는 없다. 대신 `python3 scripts/run_tests.py yangseonghwa.github.io`를 실행하면 `scripts/pages_tool.py check`가 `sims.json`·`lessons.json`·`games.json` 스키마와 모든 HTML의 메타 태그·내부 링크·용량(5MiB 이하)을 자동으로 검증한다 (D-012).

## 구조
```
projects/yangseonghwa.github.io/
  PROJECT.md             ← 이 문서
  GUIDELINES.md          ← [필수] Beflower 디자인 시스템 및 새 페이지 제작 지침서
  README.md              ← 사이트 소개와 추가 방법 (저장소 방문자용)
  no-windows-build.txt   ← exe 빌드 예외 사유 (AGENTS.md 0번, auto-build 규칙)
  assets/css/beflower.css ← 전 페이지 공통 디자인 시스템 스타일시트 (Light/Dark 토큰·헤더·푸터·컴포넌트)
  templates/             ← 신규 페이지 표준 템플릿 4종 (simulation, lesson-slides, worksheet, game)
  index.html             ← 메인 페이지
  sims.json              ← 과학 시뮬레이션 목록
  lessons.json           ← 프로그램 수업 목록
  games.json             ← 게임 목록
  wakeup.html            ← 1학년 아침 자습 루틴 안내 보드
  grade1/ grade2/        ← 학년별 과학 시뮬레이션 및 수업 발표 자료 (grade3는 아직 없음)
  grade2/star-brightness/index.html     ← 중2 별의 밝기와 등급 수업 발표(11장) + 역제곱 법칙·등급 비교 시뮬레이션
  grade2/star-color-distance/index.html ← 중2 천체의 색깔과 별까지의 거리 판별 수업 발표(10장) + 색깔·절대등급·10pc 거리 시뮬레이션
  programming/chatgpt-github-vibe/index.html     ← ChatGPT+GitHub 바이브 코딩 수업 발표(15장)
  programming/chatgpt-github-vibe/worksheet.html ← 학생 활동지(인쇄 가능)
  games/whack-a-mole/index.html                  ← 수박 터뜨리기 미니게임
  images/                ← 이미지
```

## 기술 스택 / 핵심 결정
- 순수 HTML/CSS/JavaScript, 외부 라이브러리·외부 폰트 없음 (오프라인에서도 동작). 데이터는 sims.json과 lessons.json 한 줄씩 추가하는 방식.
- Pages 전용: Windows exe를 만들 수 없고 필요도 없어 `no-windows-build.txt`로 `auto-build` 규칙의 예외를 둔다 (D-009 예외 조항). 다른 프로젝트와 의존성·빌드를 공유하지 않는다.
- 발표 페이지는 슬라이드 형식(방향키·터치·전체화면·교사 메모·인쇄). ChatGPT의 GitHub 연결 화면은 업데이트로 바뀔 수 있어 「메뉴 이름이 다를 수 있다」고 적어 둔다.

## TODO
- [x] 홈페이지에 프로그램 수업 섹션 추가 (lessons.json)
- [x] ChatGPT+GitHub 바이브 코딩 수업 발표 페이지 추가
- [x] 학생용 활동지(프롬프트 작성·수정 기록·공개 전 점검·자기 평가) 추가
- [x] 중학교 2학년 과학 「별의 밝기와 등급」 발표 자료 및 인터랙티브 시뮬레이션 추가 (`grade2/star-brightness/index.html`)
- [x] 중학교 2학년 과학 「천체의 색깔과 별까지의 거리 판별」 발표 자료 및 인터랙티브 시뮬레이션 추가 (`grade2/star-color-distance/index.html`)
- [ ] 중학교 3학년 과학 시뮬레이션 추가
- [ ] 실제 수업 전 ChatGPT의 GitHub 연결 화면을 확인하고 발표 자료의 메뉴 이름·스크린샷 보강

## 알려진 문제 / 주의사항
- `index.html`을 파일로 직접 열면(file://) 브라우저가 sims.json·lessons.json 불러오기를 막을 수 있다. 미리보기는 간단한 웹 서버(`python3 -m http.server`)로 한다.
- 이 저장소는 public이다. 시뮬레이션이나 수업 자료에 학생 개인정보·비밀번호·API 키를 넣지 말 것.
- 발표 자료는 2차시 90분 운영표와 학생 활동지를 포함한다.
- 학생 계정 사용은 연령·보호자 동의·학교 지침을 확인한다. 만 13세 미만 학생은 교사 시연과 모둠 활동으로 진행한다.
- 발표 자료의 ChatGPT 연결 메뉴는 계정·화면에 따라 바뀔 수 있으므로 실제 수업 전 교사가 확인한다.
