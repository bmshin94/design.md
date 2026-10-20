# Mint Ledger — 디자인 시스템

한 손으로 쓰는 금융 SaaS 대시보드를 위한 DESIGN.md 디자인 시스템입니다.

## 컨셉

> 출근길 지하철에서 한 손으로 쓰는 금융 대시보드.
> 흰 종이 위에 큰 숫자 하나, 그 아래 파란 버튼 하나.
> 화면은 한 번에 하나만 묻는다.

레퍼런스는 2020년대 한국 모바일 금융앱의 첫 화면입니다.
은행 지점의 대리석과 금박이 주던 권위 대신, **정확한 숫자와 빠른 응답**으로
신뢰를 만듭니다.

## 파일

| 파일 | 설명 |
|:--|:--|
| `DESIGN.md` | 디자인 시스템 본체. 토큰(YAML) + 디자인 근거(프로즈) |
| `theme.css` | Tailwind CSS v4 `@theme` 블록. `DESIGN.md`에서 자동 생성 |

## 구성

- 색상 16개 (파랑 4 · 잉크 3 · 서피스 3 · 상태 6)
- 타이포그래피 8단계 (금액용 `tnum` 고정폭 숫자 2종 포함)
- 라운딩 5단계 · 간격 6단계 · 컴포넌트 18개

모든 배경·글자 쌍이 WCAG AA(4.5:1)를 통과합니다.

```
$ npx @google/design.md lint DESIGN.md
{ "summary": { "errors": 0, "warnings": 0, "infos": 1 } }
```

## 사용법

### 1. Tailwind v4 프로젝트에 적용

`theme.css`를 메인 CSS에서 불러옵니다.

```css
/* src/app.css */
@import "tailwindcss";
@import "./theme.css";
```

그러면 토큰이 유틸리티 클래스로 바로 쓰입니다.

```html
<!-- 주 버튼 -->
<button class="bg-primary text-on-primary rounded-lg h-14 px-md
               text-label font-label hover:bg-primary-hover">
  3,200원 보내기
</button>

<!-- 지표 카드 -->
<div class="bg-surface rounded-xl p-lg">
  <p class="text-body-sm text-ink-secondary">이번 달 지출</p>
  <p class="text-numeric-xl font-numeric-xl text-ink tabular-nums">1,284,000원</p>
</div>

<!-- 상태 배지 -->
<span class="bg-success-container text-success rounded-full px-sm text-label">입금 완료</span>
<span class="bg-danger-container text-danger rounded-full px-sm text-label">한도 초과</span>
```

### 2. 토큰을 수정했을 때

`DESIGN.md`의 YAML을 고친 뒤, 검사하고 다시 내보냅니다.

```bash
npx @google/design.md lint DESIGN.md
npx @google/design.md export --format css-tailwind DESIGN.md > theme.css
```

> Windows에서 명령어가 동작하지 않으면 `designmd` 별칭을 쓰세요.
> `npx -p @google/design.md designmd lint DESIGN.md`

### 3. 다른 포맷이 필요할 때

```bash
# Tailwind v3 (tailwind.config.js 용)
npx @google/design.md export --format json-tailwind DESIGN.md > tailwind.theme.json

# 순수 CSS 변수 (Tailwind 없이)
npx @google/design.md export --format css-vars DESIGN.md > tokens.css

# W3C DTCG (Figma / Style Dictionary 연동)
npx @google/design.md export --format dtcg DESIGN.md > tokens.json
```

### 4. AI 에이전트에게 물려주기

프로젝트 루트의 `CLAUDE.md`(또는 `AGENTS.md`)에 한 줄을 추가합니다.

```md
UI 작업 시 my-design/DESIGN.md를 먼저 읽고, 토큰과 Do's and Don'ts를 따를 것.
```

토큰만 보지 말고 **프로즈를 읽게 하는 것이 핵심**입니다.
값은 무엇을 쓸지 알려주지만, 왜 그래야 하는지는 프로즈에만 있습니다.

### 5. CI에서 자동 검사

```yaml
# .github/workflows/design.yml
name: Design Lint
on: [pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: '22' }
      - run: npx @google/design.md lint my-design/DESIGN.md
```

`lint`는 에러가 있으면 종료코드 1을 반환하므로 PR이 자동으로 차단됩니다.

## 폰트 설치

Pretendard는 별도 설치가 필요합니다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css">
```

`theme.css`의 `--font-*`는 패밀리 이름만 담고 있으므로, 실제 사용 시
대체 글꼴을 함께 지정하는 것을 권합니다.

```css
@theme {
  --font-body: "Pretendard Variable", Pretendard, -apple-system, system-ui, sans-serif;
}
```

## 알아둘 점

- **줄간격은 `em` 단위로 적었습니다.** 단위 없는 숫자(`1.3`)로 쓰면
  `export`가 `--leading-*`를 내보내지 않습니다. 규격상 Dimension은
  "숫자 + 단위"여야 하기 때문입니다.
- **금액에는 `tabular-nums`를 꼭 적용하세요.** `numeric-xl`, `numeric-md`
  토큰은 `fontFeature: tnum`을 선언하지만, CSS 적용은 사용하는 쪽의 몫입니다.
  값이 갱신될 때 숫자 자리가 흔들리지 않게 해줍니다.
- **컴포넌트 토큰은 Tailwind export에 포함되지 않습니다.** 유틸리티 조합으로
  표현하는 것이 Tailwind의 방식입니다. 컴포넌트 값까지 필요하면 `dtcg`
  포맷을 쓰세요.
