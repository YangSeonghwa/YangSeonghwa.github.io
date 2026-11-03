# yangseonghwa.github.io

## 목적
Beflower(중학교 과학 교사)의 GitHub Pages 홈페이지. 학년별 과학 시뮬레이션과 프로그램(바이브 코딩) 수업 자료를 정적 웹페이지로 공개한다. **웹페이지만 있는 Pages 전용 프로젝트**이며 Windows exe는 만들지 않는다.

## 현재 상태
- 진행도: 운영 중 (https://yangseonghwa.github.io/)
- 마지막 갱신: 2026-11-03 by perplexity
- 지금 되는 것: 과학 시뮬레이션 목록(sims.json), 프로그램 수업 목록(lessons.json), 프로그램 수업 발표 페이지(programming/chatgpt-github-vibe/)
- 아직 안 되는 것: 중학교 3학년 시뮬레이션, 프로그램 수업 추가 자료
- 저장소: 이 프로젝트는 전용 GitHub 저장소(`YangSeonghwa/YangSeonghwa.github.io`, **public**)를 가진다 (D-007). 서버의 `projects/yangseonghwa.github.io/`가 그 저장소의 작업 폴더이다. 공개 저장소이고 푸시하면 Pages가 곧바로 공개하므로 개인정보·비밀·학생 정보를 절대 넣지 않는다.

## 실행 방법
```
설치: 필요 없음 (순수 HTML/CSS/JavaScript)
미리보기: python3 -m http.server   (저장소 폴더에서 실행하고 브라우저에서 localhost:8000 열기)
푸시:   git -C projects/yangseonghwa.github.io push
```
- 배포: `main` 브랜치 최상위 폴더를 GitHub Pages가 그대로 공개한다 (Settings → Pages → Deploy from a branch). 별도 빌드 단계가 없다.
- Windows exe·CI 워크플로는 없다. 테스트 파일도 없으므로 `python3 scripts/run_tests.py`에서 「테스트 없음」 경고가 나오는 것은 정상이다.

## 구조
```
projects/yangseonghwa.github.io/
  PROJECT.md             ← 이 문서
  README.md              ← 사이트 소개와 추가 방법 (저장소 방문자용)
  no-windows-build.txt   ← exe 빌드 예외 사유 (AGENTS.md 0번, auto-build 규칙)
  index.html             ← 메인 페이지
  sims.json              ← 과학 시뮬레이션 목록
  lessons.json           ← 프로그램 수업 목록
  wakeup.html            ← (기존 파일)
  grade1/ grade2/        ← 학년별 과학 시뮬레이션 (grade3는 아직 없음)
  programming/chatgpt-github-vibe/index.html  ← ChatGPT+GitHub 바이브 코딩 수업 발표(14장)
  images/                ← 이미지
```

## 기술 스택 / 핵심 결정
- 순수 HTML/CSS/JavaScript, 외부 라이브러리·외부 폰트 없음 (오프라인에서도 동작). 데이터는 sims.json과 lessons.json 한 줄씩 추가하는 방식.
- Pages 전용: Windows exe를 만들 수 없고 필요도 없어 `no-windows-build.txt`로 `auto-build` 규칙의 예외를 둔다 (D-009 예외 조항). 다른 프로젝트와 의존성·빌드를 공유하지 않는다.
- 발표 페이지는 슬라이드 형식(방향키·터치·전체화면·교사 메모·인쇄). ChatGPT의 GitHub 연결 화면은 업데이트로 바뀔 수 있어 「메뉴 이름이 다를 수 있다」고 적어 둔다.

## TODO
- [x] 홈페이지에 프로그램 수업 섹션 추가 (lessons.json)
- [x] ChatGPT+GitHub 바이브 코딩 수업 발표 페이지 추가
- [ ] 실제 수업 전 ChatGPT의 GitHub 연결 화면을 확인하고 발표 자료의 메뉴 이름·스크린샷 보강
- [ ] 학생용 활동지(프롬프트 작성 시트) 추가
- [ ] 중학교 3학년 과학 시뮬레이션 추가

## 알려진 문제 / 주의사항
- `index.html`을 파일로 직접 열면(file://) 브라우저가 sims.json·lessons.json 불러오기를 막을 수 있다. 미리보기는 간단한 웹 서버(`python3 -m http.server`)로 한다.
- 이 저장소는 public이다. 시뮬레이션이나 수업 자료에 학생 개인정보·비밀번호·API 키를 넣지 말 것.
- 발표 자료의 ChatGPT 연결 방법은 작성 시점(2026-11)의 안내 기준이라 화면이 바뀌면 갱신이 필요하다.
