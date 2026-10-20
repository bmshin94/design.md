---
version: alpha
name: Mint Ledger
description: 한 손으로 쓰는 금융 SaaS 대시보드를 위한 디자인 시스템
colors:
  primary: "#1B64DA"
  primary-hover: "#1550B8"
  primary-container: "#E8F1FE"
  on-primary: "#FFFFFF"
  surface: "#FFFFFF"
  surface-subtle: "#F2F4F6"
  border: "#E5E8EB"
  ink: "#191F28"
  ink-secondary: "#4E5968"
  ink-tertiary: "#6B7684"
  success: "#0B7A52"
  success-container: "#E7F6EF"
  warning: "#8A5300"
  warning-container: "#FFF4E0"
  danger: "#C62828"
  danger-container: "#FDECEC"
typography:
  display:
    fontFamily: Pretendard
    fontSize: 2rem
    fontWeight: "700"
    lineHeight: 1.3em
    letterSpacing: -0.02em
  heading-lg:
    fontFamily: Pretendard
    fontSize: 1.5rem
    fontWeight: "700"
    lineHeight: 1.35em
    letterSpacing: -0.015em
  heading-md:
    fontFamily: Pretendard
    fontSize: 1.25rem
    fontWeight: "600"
    lineHeight: 1.4em
    letterSpacing: -0.01em
  body:
    fontFamily: Pretendard
    fontSize: 1rem
    fontWeight: "400"
    lineHeight: 1.6em
  body-sm:
    fontFamily: Pretendard
    fontSize: 0.875rem
    fontWeight: "400"
    lineHeight: 1.55em
  label:
    fontFamily: Pretendard
    fontSize: 0.8125rem
    fontWeight: "600"
    lineHeight: 1.4em
  numeric-xl:
    fontFamily: Pretendard
    fontSize: 2.25rem
    fontWeight: "700"
    lineHeight: 1.2em
    letterSpacing: -0.025em
    fontFeature: "tnum"
  numeric-md:
    fontFamily: Pretendard
    fontSize: 1rem
    fontWeight: "600"
    lineHeight: 1.45em
    fontFeature: "tnum"
rounded:
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  2xl: 48px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label}"
    rounded: "{rounded.lg}"
    padding: 16px
    height: 56px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
  button-secondary:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.primary}"
    typography: "{typography.label}"
    rounded: "{rounded.lg}"
    padding: 16px
    height: 56px
  button-ghost:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-secondary}"
    typography: "{typography.label}"
    rounded: "{rounded.md}"
    padding: 12px
  input-field:
    backgroundColor: "{colors.surface-subtle}"
    textColor: "{colors.ink}"
    typography: "{typography.body}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 56px
  input-field-placeholder:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-tertiary}"
    typography: "{typography.body}"
  card-metric:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    typography: "{typography.numeric-xl}"
    rounded: "{rounded.xl}"
    padding: 24px
  card-metric-label:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-secondary}"
    typography: "{typography.body-sm}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  table-header:
    backgroundColor: "{colors.surface-subtle}"
    textColor: "{colors.ink-secondary}"
    typography: "{typography.label}"
    padding: 12px
  table-cell:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink}"
    typography: "{typography.numeric-md}"
    padding: 12px
  nav-item:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.ink-secondary}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.md}"
    padding: 12px
  nav-item-active:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.primary}"
    typography: "{typography.label}"
    rounded: "{rounded.md}"
    padding: 12px
  badge-success:
    backgroundColor: "{colors.success-container}"
    textColor: "{colors.success}"
    typography: "{typography.label}"
    rounded: "{rounded.full}"
    padding: 8px
  badge-warning:
    backgroundColor: "{colors.warning-container}"
    textColor: "{colors.warning}"
    typography: "{typography.label}"
    rounded: "{rounded.full}"
    padding: 8px
  badge-danger:
    backgroundColor: "{colors.danger-container}"
    textColor: "{colors.danger}"
    typography: "{typography.label}"
    rounded: "{rounded.full}"
    padding: 8px
  toast-success:
    backgroundColor: "{colors.success}"
    textColor: "{colors.on-primary}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.md}"
    padding: 16px
  toast-danger:
    backgroundColor: "{colors.danger}"
    textColor: "{colors.on-primary}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.md}"
    padding: 16px
---

## Overview

출근길 지하철에서 한 손으로 쓰는 금융 대시보드.

사용자는 흔들리는 객차 안에서 엄지 하나로 이번 달 지출을 확인하고, 이상 거래
알림을 넘긴다. 양손을 쓸 수 있는 상황이 아니고, 설명서를 읽을 시간도 없다.

레퍼런스는 2020년대 한국 모바일 금융앱의 첫 화면이다. 흰 종이 위에 큰 숫자
하나, 그 아래 파란 버튼 하나. 화면은 한 번에 하나만 묻는다. 두 가지를 동시에
물으면 사용자는 둘 다 답하지 않는다.

이것은 "금융"처럼 보이려는 디자인이 아니다. 은행 지점의 대리석, 금박, 세리프
로고가 주던 권위는 여기에 없다. 신뢰는 장식이 아니라 **정확한 숫자와 빠른
응답**에서 온다. 화면이 조용할수록 사용자는 안심한다.

## Colors

흰 종이와 회색 잉크, 그리고 행동을 요구하는 파랑 하나.

- **Primary** {colors.primary} — 다음 행동을 가리키는 유일한 색. 한 화면에
  파란 버튼은 하나만 둔다. 둘이 되는 순간 둘 다 힘을 잃는다.
- **Primary hover** {colors.primary-hover} — 눌리는 순간에만 나타난다.
- **Primary container** {colors.primary-container} — 선택된 메뉴, 보조 버튼의
  배경. 파랑의 존재를 약하게 암시할 때 쓴다.
- **Ink** {colors.ink} — 모든 숫자와 제목. 순흑이 아닌 남빛 먹색이라 흰 바탕
  위에서 눈을 덜 찌른다.
- **Ink secondary** {colors.ink-secondary} — 항목 이름, 표 머리글, 설명.
- **Ink tertiary** {colors.ink-tertiary} — 입력 전 안내 문구와 비활성 상태.
  이 색이 본문에 쓰이면 그 문장은 읽히지 않는다는 뜻이다.
- **Surface** {colors.surface} — 카드와 본문의 바탕. 기본은 순백이다.
- **Surface subtle** {colors.surface-subtle} — 입력창과 표 머리글의 바탕.
  테두리를 그리는 대신 바탕을 눌러 영역을 만든다.
- **Border** {colors.border} — 1px 구분선 전용. 카드 테두리로는 쓰지 않는다.

상태 색은 세 쌍으로만 존재한다. 짙은 색은 글자, 연한 색은 배경이다.

- **Success** {colors.success} / {colors.success-container} — 입금, 승인, 정상.
- **Warning** {colors.warning} / {colors.warning-container} — 확인 필요, 보류.
- **Danger** {colors.danger} / {colors.danger-container} — 실패, 한도 초과,
  이상 거래. 이 색은 사용자가 돈을 잃을 수 있을 때만 쓴다.

모든 배경·글자 쌍은 WCAG AA(4.5:1)를 넘긴다. 금융 화면에서 읽히지 않는 숫자는
없는 숫자와 같다.

## Typography

Pretendard 한 가족으로 끝낸다. 한글과 숫자가 같은 리듬으로 흐르는 것이
이 시스템의 전부다.

- **Numeric XL** {typography.numeric-xl} — 화면의 주인공. 잔액, 이번 달 합계
  같은 단 하나의 숫자. `tnum`(고정폭 숫자)을 켜서 값이 갱신될 때 자리가
  흔들리지 않게 한다.
- **Numeric MD** {typography.numeric-md} — 표 안의 금액. 역시 `tnum`.
  소수점과 쉼표가 열 단위로 정렬되어야 눈이 세로로 훑을 수 있다.
- **Display** {typography.display} / **Heading LG** {typography.heading-lg} /
  **Heading MD** {typography.heading-md} — 페이지, 섹션, 카드 제목.
- **Body** {typography.body} / **Body SM** {typography.body-sm} — 본문과 설명.
- **Label** {typography.label} — 버튼, 배지, 표 머리글. 대문자 변환은 하지
  않는다. 한글에 대문자는 없고, 영문만 대문자로 만들면 둘의 높이가 어긋난다.

크기 차이는 소박하게 둔다. 가장 큰 숫자가 본문의 2.25배일 뿐이다.
위계는 크기보다 **여백과 위치**로 만든다.

## Layout

- 기준 단위는 {spacing.sm} 8px이다. 모든 간격은 8의 배수로 떨어진다.
- 카드 안쪽 여백은 {spacing.lg}, 카드 사이는 {spacing.md}, 섹션 사이는
  {spacing.2xl}.
- 모바일에서 좌우 가장자리 여백은 {spacing.md}를 깨지 않는다. 숫자가 화면
  끝에 붙으면 잘린 것처럼 보인다.
- 터치 대상의 높이는 최소 56px이다. 엄지로 누르는 화면에서 44px은 좁다.
- 한 화면에 카드는 넷까지. 다섯 번째부터는 스크롤이 아니라 다음 화면이다.
- 표는 모바일에서 표를 포기한다. 열이 셋을 넘으면 카드 목록으로 바꾼다.

## Elevation & Depth

그림자는 **떠 있는 것에만** 쓴다. 토스트, 바텀시트, 드롭다운 셋뿐이다.

- 카드는 떠 있지 않다. 카드는 종이 위에 인쇄된 영역이고, 구분은 여백과
  둥근 모서리로 충분하다.
- 그림자를 쓸 때는 흐림 반경을 넓게, 농도를 낮게. 경계가 보이는 그림자는
  2015년 머티리얼 디자인의 흔적이다.
- 깊이의 단계는 둘뿐이다. 바닥(종이)과 그 위(떠 있는 것).
  세 번째 층이 필요하다고 느껴지면 화면 구조가 잘못된 것이다.

## Shapes

둥근 모서리는 이 시스템의 성격이다. 각진 모서리는 쓰지 않는다.

- {rounded.sm} 8px — 작은 칩, 아이콘 배경
- {rounded.md} 12px — 입력창, 메뉴 항목, 토스트
- {rounded.lg} 16px — 버튼
- {rounded.xl} 24px — 카드, 바텀시트
- {rounded.full} — 상태 배지와 아바타

**바깥이 안보다 더 둥글다.** 24px 카드 안에 16px 버튼이 들어간다.
이 관계가 뒤집히면 요소가 카드에서 떠 보인다.

## Components

- **Button primary** — 화면의 유일한 파란 버튼. 모바일에서는 화면 하단에
  가로로 꽉 채운다. 레이블은 "확인"이 아니라 "3,200원 보내기"처럼
  **결과를 말한다**.
- **Button secondary** — 연한 파랑 배경. "나중에 하기", "다른 계좌 선택"처럼
  주된 행동이 아닌 선택지.
- **Button ghost** — 텍스트만 있는 버튼. 취소와 닫기.
- **Input field** — 회색 바탕, 테두리 없음. 금액 입력은 숫자 키패드를 띄우고
  천 단위 쉼표를 입력 중에 넣는다.
- **Card metric** — 지표 하나당 카드 하나. 위에 작은 회색 레이블
  ({typography.body-sm}), 아래에 큰 숫자({typography.numeric-xl}).
  이 순서를 바꾸지 않는다. 사용자는 숫자를 먼저 보고 레이블로 확인한다.
- **Table header / cell** — 금액 열은 오른쪽 정렬, 나머지는 왼쪽.
- **Nav item / active** — 선택된 항목만 연한 파랑 배경을 갖는다.
- **Badge** — 거래 상태. 성공·확인필요·실패 셋뿐이고, 네 번째 상태를
  만들고 싶으면 그건 배지가 아니라 설명이 필요한 일이다.
- **Toast** — 화면 상단에서 내려와 3초 후 사라진다. 사용자가 닫을 수
  있어야 한다.

## Do's and Don'ts

- **Don't** 한 화면에 파란 버튼을 둘 이상 두지 마라. 두 개의 주된 행동은
  주된 행동이 없다는 뜻이다.
- **Don't** 그라데이션을 쓰지 마라. 카드에도, 버튼에도, 배경에도. 종이에는
  빛이 없다.
- **Don't** 숫자에 애니메이션으로 카운트업 효과를 주지 마라. 잔액은 공연이
  아니다. 사용자는 값을 읽으러 왔다.
- **Don't** 금액을 비례 폭 숫자로 쓰지 마라. 갱신될 때 자리가 흔들린다.
  `tnum`은 선택이 아니다.
- **Don't** 성공을 알리려고 danger 색 근처의 빨강을 쓰지 마라. 금융에서
  빨강은 손실이다.
- **Don't** 카드에 그림자를 넣지 마라. 카드는 떠 있지 않다.
- **Don't** 비활성 버튼을 흐릿한 파랑으로 만들지 마라. 눌릴 것처럼 보인다.
  비활성은 회색이다.
- **Don't** 로딩 중에 레이아웃이 움직이게 하지 마라. 자리를 미리 비워 둔다.
- **Do** 화면이 한 번에 하나만 묻게 하라. 질문이 둘이면 화면을 쪼갠다.
- **Do** 버튼 레이블에 결과를 써라. "확인"보다 "이 계좌로 보내기"가 짧다.
- **Do** 숫자를 크게, 설명을 작게. 위계를 의심하면 숫자를 믿어라.
- **Do** 여백을 남겨라. 화면 아래 삼분의 일이 비어 있는 것은 정상이다.
- **Do** 실패했을 때 무엇을 하면 되는지 같은 화면에서 말하라. 사용자를
  고객센터로 보내는 것은 설계의 실패다.
