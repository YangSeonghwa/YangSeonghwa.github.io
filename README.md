# 🌸 Beflower의 과학 시뮬레이션 랩

중학교 과학 교사 **Beflower**가 AI와 함께 바이브 코딩으로 만드는 학년별 과학 웹 시뮬레이션 모음입니다.

## 구조

```
index.html        # 메인 페이지
grade1/           # 중1 시뮬레이션 (예: grade1/force/index.html)
grade2/           # 중2 시뮬레이션
grade3/           # 중3 시뮬레이션
```

## 새 시뮬레이션 추가 방법

1. `gradeN/주제명/index.html` 위치에 시뮬레이션 업로드
2. `index.html`의 `SIMS` 배열에 한 줄 추가

```js
{ grade:1, area:"물리", title:"힘의 합성", desc:"두 힘의 합력 관찰", url:"grade1/force/index.html" }
```

## 배포

Settings → Pages → Branch `main` / root 선택
