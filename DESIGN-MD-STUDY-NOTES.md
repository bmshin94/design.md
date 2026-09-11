# DESIGN.md 분석 노트

> 이 레포(DESIGN.md)가 무엇이고, 어떻게 쓰며, 어떤 기회가 있는지 정리한 학습 노트입니다.
> 모든 기술적 사실은 이 저장소의 소스코드를 직접 확인해서 작성했습니다.

## 🔗 관련 주소

| 항목 | 주소 |
|:--|:--|
| 내 저장소 (fork) | https://github.com/bmshin94/design.md |
| 원본 저장소 (Google) | https://github.com/google-labs-code/design.md |
| npm 패키지 | https://www.npmjs.com/package/@google/design.md |
| 이슈 트래커 (원본) | https://github.com/google-labs-code/design.md/issues |
| 참고: W3C 디자인 토큰 포맷 | https://www.designtokens.org/ |

---

## 1. 이게 뭔가요?

한 줄 요약: **AI(코딩 에이전트)에게 주는 "우리 프로젝트 디자인 규칙 메모장" 포맷**입니다.

### 해결하려는 문제

AI는 대화가 끝나면 기억을 잃습니다. 그래서 같은 프로젝트인데도 요청할 때마다
버튼 색이 다르고, 폰트가 바뀌고, 여백이 제각각인 화면이 나옵니다.

`DESIGN.md` 파일을 프로젝트에 두면, 어떤 AI 도구를 쓰든(Claude Code, Cursor, Gemini 등)
같은 파일을 읽기 때문에 결과물의 톤앤매너가 유지됩니다.

### 파일 구조 — 두 개의 층

```md
---
name: Heritage              ← ① YAML 프론트매터: 기계가 읽는 정확한 값(토큰)
colors:
  primary: "#1A1C1E"
  tertiary: "#B8422E"
typography:
  h1:
    fontFamily: Public Sans
    fontSize: 3rem
---

## Colors                   ← ② 마크다운 본문: 사람과 AI가 읽는 "이유"(프로즈)

팔레트는 고대비 중성색과 단 하나의 강조색에 뿌리를 둔다.

- **Primary (#1A1C1E):** 헤드라인과 본문 텍스트를 위한 딥 잉크.
- **Tertiary (#B8422E):** "보스턴 클레이" — 오직 인터랙션에만 쓰인다.
```

- **토큰(위)** = 정확한 값. 규범적(normative) 값.
- **프로즈(아래)** = 그 값이 왜 존재하고 어떻게 적용하는지의 맥락.

### 핵심 철학 (PHILOSOPHY.md)

> **"디자인 퀄리티는 값의 정밀함보다, 의도가 얼마나 명확히 서술됐는지가 결정한다."**

이 문서에서 가장 중요한 두 가지 원칙:

1. **구체적 레퍼런스 > 형용사 나열**
   - "모던하고, 깔끔하고, 신뢰감 있고, 프리미엄한" → **영역(region)**을 묘사함.
     모델은 그 영역의 한가운데, 즉 가장 평범한 결과를 만듭니다.
   - "1970년대 명문대 대학원 세미나 유인물" → **점(point)**을 찍음.
     여백, 서체 크기, 장식 없음까지 한 문장이 전부 담고 있습니다.

2. **네거티브 제약은 공짜로 따라온다**
   - 레퍼런스가 충분히 구체적이면 "하지 말 것"은 저절로 정해집니다.
     강의 유인물은 빛나지 않고 그라데이션을 쓰지 않는다는 걸 모델이 이미 압니다.
   - 다만 의도적인 Do's and Don'ts 목록은 여전히 유용합니다.
     장황한 금지 목록이 필요하다면, 그건 설명이 모호했다는 신호입니다.

3. **포맷은 스펙이 아니라 사용자를 통해 자란다**
   - 스펙은 최소한(name, colors, typography, spacing, rounded, components)만 정의하고,
     motion·iconography·elevation 같은 건 사용자가 자유롭게 추가할 수 있습니다.
   - 린터는 모르는 키를 에러로 막지 않습니다. 토큰은 "명령"이 아니라 "맥락"이기 때문입니다.

---

## 2. 폴더 구조

| 경로 | 역할 |
|:--|:--|
| `README.md` | 포맷 요약 + CLI 전체 레퍼런스 |
| `PHILOSOPHY.md` | 왜 이렇게 설계했는지 (가장 읽을 가치 있는 문서) |
| `docs/spec.md` | 공식 규격서 (자동 생성됨 — 직접 수정 금지) |
| `packages/cli/` | 실제 알맹이. TypeScript로 만든 린터 + 익스포터 |
| `packages/cli/src/commands/` | `lint` / `diff` / `export` / `spec` 4개 명령어 |
| `packages/cli/src/linter/linter/rules/` | 린트 규칙 11개 (규칙 1개 = 파일 1개) |
| `packages/cli/src/linter/spec-gen/` | `spec.mdx` → `docs/spec.md` 자동 생성기 |
| `examples/` | 완성 예제 3개 (`paws-and-paths`, `atmospheric-glass`, `totality-festival`) |
| `.agents/skills/` | 이 레포를 **개발할 때 쓴** AI 스킬 4개 |
| `.github/workflows/test.yml` | CI 테스트 자동화 |
| `CLAUDE.md` | 내(사용자)가 추가한 AI 페르소나 설정 파일 |

### 눈여겨볼 점

- **`.agents/skills/`** — `tdd`, `ink`, `agent-dx-cli-scale`, `typed-service-contracts`.
  구글 팀도 AI에게 스킬을 물려서 이 도구를 개발했다는 증거입니다.
  구조가 `CLAUDE.md`와 동일합니다 (`---` 프론트매터에 `name` + `description`).
- **모든 소스 파일이 `*.ts` ↔ `*.test.ts` 1:1 페어** — TDD로 작성됨.
- **예제가 딱 3개** (각 210~219줄). 전 세계 공개 예제가 이게 전부라는 뜻입니다.

---

## 3. 설치 및 사용법

### 설치

```bash
# 방법 A: 설치 없이 바로 (가장 쉬움)
npx @google/design.md lint DESIGN.md

# 방법 B: 프로젝트에 고정
npm install @google/design.md
```

#### ⚠️ Windows 주의사항

`design.md`의 `.md` 확장자를 윈도우가 "마크다운 파일"로 인식해서,
명령어가 실행되지 않고 마크다운 에디터가 열릴 수 있습니다.
이때는 **점 없는 별칭 `designmd`**를 사용하세요 (동일한 진입점입니다).

```bash
npx -p @google/design.md designmd lint DESIGN.md
```

package.json 스크립트에서도 마찬가지입니다:

```jsonc
{ "scripts": { "design:lint": "designmd lint DESIGN.md" } }
```

#### `npm error ENOVERSIONS` 가 뜬다면

npm이 공개 레지스트리를 보고 있지 않다는 뜻입니다.

```bash
npm config get registry   # https://registry.npmjs.org/ 여야 정상
npm cache clean --force   # 404가 캐시됐다면
```

### 이 저장소를 직접 실행 (bun 기반)

```bash
bun install
bun run cli lint examples/paws-and-paths/DESIGN.md   # 예제로 테스트
bun test                                             # 테스트 실행
bun run build                                        # 빌드
```

### 명령어 4종

```bash
# ① lint — 구조 검증 (문제 있으면 exit code 1 → CI에서 차단 가능)
npx @google/design.md lint DESIGN.md
cat DESIGN.md | npx @google/design.md lint -

# ② diff — 두 버전 비교, 품질 저하(regression) 판정
npx @google/design.md diff DESIGN.md DESIGN-v2.md

# ③ export — 토큰을 실제 코드 포맷으로 변환
npx @google/design.md export --format css-tailwind DESIGN.md > theme.css
npx @google/design.md export --format json-tailwind DESIGN.md > tailwind.theme.json
npx @google/design.md export --format dtcg DESIGN.md > tokens.json

# ④ spec — 규격서 출력 (AI 프롬프트에 주입용)
npx @google/design.md spec
npx @google/design.md spec --rules-only --format json
```

### 린트 규칙 11개

| 규칙 | 심각도 | 검사 내용 |
|:--|:--|:--|
| `broken-ref` | error | `{colors.primary}` 참조가 실제 토큰에 없음 |
| `contrast-ratio` | warning | 배경/글자색 대비가 WCAG AA(4.5:1) 미달 |
| `missing-primary` | warning | 색은 있는데 `primary`가 없음 |
| `missing-typography` | warning | 색은 있는데 타이포그래피가 없음 |
| `orphaned-tokens` | warning | 정의만 하고 아무데서도 안 쓰는 색 |
| `section-order` | warning | 섹션이 규격 순서를 벗어남 |
| `unknown-key` | warning | 오타로 보이는 최상위 키 (`colours:` → `colors:`) |
| `token-like-ignored` | warning | 모르는 키인데 토큰처럼 생긴 값이 들어있음 |
| `token-summary` | info | 섹션별 토큰 개수 요약 |
| `missing-sections` | info | 선택 섹션(spacing, rounded) 누락 |
| `omitted-rules` | info | `omitted` 설정 검증 |

### 섹션 순서 (있는 것만 이 순서를 지켜야 함)

`Overview` → `Colors` → `Typography` → `Layout` → `Elevation & Depth` → `Shapes` → `Components` → `Do's and Don'ts`

### 라이브러리로 쓰기

```typescript
import { lint } from '@google/design.md/linter';

const report = lint(markdownString);
report.findings;      // Finding[]
report.summary;       // { errors, warnings, info }
report.designSystem;  // 파싱된 DesignSystemState
```

---

## 4. 플러그인? 스킬? MCP?

**셋 다 아닙니다.** 정체는 **"파일 포맷 + CLI 도구"** 입니다.
`.json` 포맷이나 `eslint` 같은 존재라고 보면 됩니다.

| | 정체 | 비유 |
|:--|:--|:--|
| 플러그인 | 특정 앱에 끼우는 부품 | 게임 MOD |
| 스킬 | AI에게 주는 작업 설명서 | 레시피 카드 |
| MCP | AI ↔ 외부 도구 통신 규약 | 콘센트 규격 |
| **DESIGN.md** | **포맷 + CLI** | **`.json` / `eslint`** |

다만 **"AI가 쓰라고 만든 CLI"** 입니다. 소스코드에 이렇게 적혀 있습니다:

> "Agent-first CLI for DESIGN.md — the hands and eyes for design system work."

출력이 전부 JSON인 것도, `spec` 명령이 존재하는 것도 전부 에이전트가 소비하기 위함입니다.

### 참고: 레포 안의 `.agents/skills/`

이건 DESIGN.md의 기능이 아니라, **이 레포를 개발할 때 쓴 개발용 AI 스킬**입니다.
혼동하지 마세요. 다만 에이전트 설계를 배우기엔 아주 좋은 교보재입니다.

> **기회:** MCP 서버가 아니라는 건, 누군가 MCP로 감쌀 수 있다는 뜻입니다. (→ 6장)

---

## 5. API 토큰이 필요한가?

### 전혀 필요 없습니다. 완전 무료입니다.

소스코드를 직접 검색해 확인한 결과:

```
fetch / axios / node-fetch / https.request  →  0건
API_KEY / apiKey / Authorization            →  0건
process.env 사용                             →  테스트 파일의 PATH 설정뿐
```

**네트워크 연결조차 하지 않습니다.** AI가 내장돼 있지 않고,
파일을 읽어서 텍스트를 분석하고 색 대비를 수학적으로 계산할 뿐인 순수 계산 프로그램입니다.

런타임 의존성도 9개뿐입니다:
`citty`(CLI), `remark-*`/`unified`/`unist-util-visit`(마크다운), `yaml`, `zod`(검증)

### 그래서 좋은 점

- 비용 0원, 토큰 소모 0
- 디자인 내용이 외부로 나가지 않음 → 사내/보안 프로젝트에서도 안전
- 빠름 (API 대기 없음), 오프라인 동작

---

## 6. 왜 GitHub에서 화제인가?

> 주의: 정확한 스타 수는 이 노트 작성 시점에 확인하지 않았습니다. 아래는 내용 기반 분석입니다.

1. **타이밍** — 바이브코딩 대중화로 "AI 결과물이 매번 달라진다"는 문제가 폭발했는데,
   모두가 겪지만 아무도 안 풀던 문제를 정면으로 다룹니다.
2. **이름** — `README.md`, `CLAUDE.md`, `AGENTS.md` 계보에 자연스럽게 합류.
   설명 없이도 뭔지 이해됩니다.
3. **Google 브랜드** — `google-labs-code` 조직 + npm `@google` 스코프.
   "표준이 될 수도 있다"는 기대를 만듭니다.
4. **PHILOSOPHY.md가 잘 쓰였음** — "형용사는 영역을, 구체적 레퍼런스는 점을 묘사한다"처럼
   공유하기 좋은 문장이 많아 SNS 확산에 유리합니다.
5. **진입장벽 0** — 설치·토큰·가입 없이 `npx` 한 줄.

### 냉정한 평가

- 아직 `alpha` 버전이고 README에 "포맷이 바뀔 수 있다"고 명시돼 있습니다.
- 최근 커밋들이 오타 수정, 윈도우 호환성 등 기초 공사 단계입니다.
- **스타 수 > 실사용자 수**일 가능성이 큽니다.
- 다만 그건 생태계가 비어있다는 뜻이므로, 먼저 채우는 쪽에 기회가 있습니다.

---

## 7. 로컬 에이전트 구축에 도움이 되는가?

### A. 부품으로 쓰기

에이전트에게 "디자인 감각"과 "자기검증 능력"을 붙여주는 용도입니다.

```
사용자: "회원가입 페이지 만들어줘"
  → 에이전트가 DESIGN.md 읽음
  → 코드 생성
  → lint 실행으로 자가검증
  → ❌ "대비 3.2:1, 접근성 위반" 발견
  → 스스로 수정 후 재검사
  → ✅ 통과
```

이 **자가수정 루프**가 핵심입니다. 일반 린터는 사람이 읽는 텍스트를 출력하지만,
이건 JSON을 출력해서 에이전트가 파싱 후 바로 행동할 수 있습니다.

적용 3단계:
1. `npx @google/design.md spec` 결과를 시스템 프롬프트에 주입
2. `lint` / `export`를 에이전트의 도구(tool)로 등록
3. 코드 수정 후 자동 lint 훅 설정

### B. 교보재로 쓰기 (사실 이쪽이 더 값질 수 있음)

| 배울 점 | 위치 |
|:--|:--|
| 명령어 분리 설계 | `src/commands/` 4개 |
| 규칙 1개 = 파일 1개 (플러그인 구조) | `linter/rules/` 11개 |
| 소스 ↔ 테스트 1:1 페어링 (TDD) | 전 디렉터리 |
| 스펙을 코드로 자동 생성 | `spec-gen/` (`spec.mdx` → `spec.md`) |
| AI 개발 워크플로우 | `.agents/skills/agent-dx-cli-scale` 등 |

### 한계

- 디자인 영역만 담당합니다. 에이전트의 두뇌·기억·툴호출은 별도 구현이 필요합니다.
- alpha라 포맷 변경 가능성이 있어, 너무 깊게 결합하면 유지보수 부담이 생깁니다.

---

## 8. 수익화 아이디어

### 8-0. 먼저 — 법적으로 팔아도 되는가?

**라이선스: Apache 2.0. 상업적 이용이 가능합니다.**

| 가능 | 의무 |
|:--|:--|
| 상업적 이용 | 라이선스 사본 포함 |
| 수정 | 수정한 파일에 "변경함" 표시 |
| **비공개 배포 (소스 공개 의무 없음)** | 저작권·특허·상표 고지 유지 |
| 특허 사용권 포함 | NOTICE 파일 있으면 포함 (※ 확인 결과 이 레포엔 NOTICE 파일 **없음**) |

#### ⚠️ 가장 조심할 것 — 상표 (라이선스 6조)

> "이 라이선스는 라이선서의 상호, 상표, 서비스 마크, 제품명 사용 권한을 부여하지 않는다."

| 금지 | 허용 |
|:--|:--|
| "**Google** Design Kit" | "DESIGN.md 템플릿 팩" |
| 구글 로고 사용 | "Powered by the DESIGN.md format" |
| "구글 공식 파트너" 표현 | "Built on the open DESIGN.md spec (Apache 2.0)" |
| `@google/...` 유사 패키지명 | `@myname/design-md-mcp` |

#### 중요한 사실

**내가 직접 작성한 `DESIGN.md` 파일 자체는 100% 내 저작물입니다.**
포맷은 규격일 뿐이고, 그 안에 채운 색 조합·타이포·산문은 창작물입니다.
(레시피 "형식"은 공용이지만, 내가 쓴 레시피는 내 것인 것과 같습니다.)
→ 그래서 템플릿 판매가 법적으로 가장 깨끗합니다.

### 8-1. 시장 구조

| 대상 | 고충 | 지불 의향 |
|:--|:--|:--|
| 1인 개발자 / 인디해커 | "디자인 감각은 없는데 앱은 예뻐야 함" | $10~50 (1회) |
| 스타트업 팀 (5~30명) | "사람마다 AI 결과물이 달라 난장판" | $20~100/월 |
| 중견기업 / 공공 | "웹접근성 위반 시 법적 리스크" | $500~5,000/월 |

위로 갈수록 금액은 크지만 진입이 어렵습니다. 아래에서 시작해 올라가는 것이 정석입니다.

### 8-2. 아이디어 7개

#### 🥇 ① 프리미엄 템플릿 팩 판매
**난이도 ⭐☆☆☆☆ | 시작까지 3~7일 | 가장 현실적**

구글 예제 구조를 그대로 상품 포맷으로 씁니다:

```
K-Commerce Design Pack/
├── DESIGN.md            (본체, 200줄 내외)
├── README.md            (사용법)
├── design_tokens.json   (Figma / Style Dictionary 연동용)
├── tailwind.config.js   (Tailwind v3)
├── theme.css            (Tailwind v4 — export 명령으로 자동 생성)
├── preview/             (스크린샷 3~5장 — 매출에 가장 큰 영향)
└── LICENSE.txt          (구매자 이용 범위)
```

만들 만한 팩 (한국 특화가 차별점):
K-Commerce(무신사 결) / 핀테크(토스 결) / 배달앱 / 병원·클리닉 /
뉴스레터 / 게임 대시보드 / 브루탈리즘 / 학술 리포트

가격 설계:
```
단품 $19 · 번들 5개 $59(주력) · 전체+평생업데이트 $149 · 팀 $299
```

**핵심 차별화는 프로즈입니다.** 토큰만 예쁘게 뽑으면 아무도 사지 않습니다.

```md
[나쁜 예] 모던하고 깔끔한 이커머스 디자인입니다.

[좋은 예] 2010년대 후반 서울 성수동의 편집샵 룩북.
제품이 주인공이고 UI는 액자다. 사진은 여백 없이 가장자리까지 꽉 차게,
텍스트는 그 아래에서 조용히 물러난다.
할인 배지는 빨강이 아니라 먹색이다 — 우리는 싸다고 소리치지 않는다.

## Do's and Don'ts
- **Don't** 그라데이션 버튼. 2015년 쇼핑몰의 냄새가 난다.
- **Don't** 별점을 노란 별로 그리지 마라. 숫자로 충분하다.
- **Do** 사진 위에 텍스트를 얹지 마라. 사진은 사진, 글은 글.
```

판매처: Gumroad(~10%, 가장 쉬움) / Lemon Squeezy(~5%, VAT 자동) / 크몽 / 자체 사이트(Stripe)

리스크: 재판매 → 라이선스 문구 + 워터마크 프리뷰로 방어. 최소 5개는 있어야 "가게"가 됩니다.

#### 🥈 ② MCP 서버로 감싸기
**난이도 ⭐⭐☆☆☆ | 2~3주 | 직접수익은 낮지만 전략적 가치 최고**

DESIGN.md는 MCP가 아니므로, 그 빈자리를 채웁니다.

```
design-md-mcp
├── lint_design    "이 DESIGN.md 검사해줘"
├── export_theme   "Tailwind CSS로 뽑아줘"
├── diff_design    "v1이랑 v2 비교해줘"
├── get_spec       "규격 알려줘"
└── design://current  (리소스: 현재 프로젝트 디자인 읽기)
```

린터가 라이브러리로 공개돼 있어 엔진을 다시 짤 필요가 없습니다:

```js
import { lint } from '@google/design.md/linter';
const report = lint(content);
return { findings: report.findings, summary: report.summary };
```

수익 모델: 오픈소스 무료 배포 → 인지도 확보 → 유료 클라우드(팀 저장소, 동기화) $15/유저/월.
**진짜 목적은 "DESIGN.md = 이 사람" 포지션 선점**이며, 그게 ①과 ④를 띄웁니다.

#### 🥉 ③ Figma ↔ DESIGN.md 변환 플러그인
**난이도 ⭐⭐⭐☆☆ | 1~2개월**

양방향이 핵심입니다. 특히 **DESIGN.md → Figma** 역방향이 임팩트가 큽니다
(AI가 만든 디자인을 디자이너가 피그마에서 확인).

기술 힌트: `export --format dtcg`가 이미 DTCG 표준 JSON을 출력합니다.
DTCG는 Figma·Style Dictionary가 읽는 표준이라 다리의 절반은 이미 놓여 있습니다.

가격: Free(색상만) / Pro $9월(전체 토큰 + AI 프로즈 생성) / Team $29월
장점: Figma Community 자체가 노출 채널 → 마케팅 비용 0
리스크: Figma가 직접 구현하면 끝 → AI 프로즈 생성 등으로 차별화 필요

#### ④ "디자인 CI" SaaS — PR 자동 검사 봇
**난이도 ⭐⭐⭐⭐☆ | 3~6개월 | 수익 잠재력 최대**

```
🤖 DesignGuard bot commented:

⚠️ 접근성 경고 2건
  • components.button-cta
    글자(#FFB800) / 배경(#FFFFFF) 대비 1.8:1 → WCAG AA 미달 ❌
    제안: #B37E00 으로 변경 시 4.6:1 ✅
  • 토큰 참조 오류: {colors.accent} 미정의

📉 이전 버전 대비 경고 +2 → regression 감지
```

핵심 로직이 이미 존재합니다:
색 대비 계산(`contrast-ratio`), 참조 검증(`broken-ref`),
**품질 저하 판정(`diff`의 `regression: true`)**, JSON 출력.
직접 만들 부분은 GitHub 연동 + 결제 + 대시보드뿐입니다.

돈이 되는 이유는 **법적 리스크**입니다:
한국 장애인차별금지법/웹접근성 품질인증, 미국 ADA 소송,
EU European Accessibility Act(2025 시행).

가격: Free(오픈소스) / Team $29월 / Business $99월 / Enterprise 견적(온프레미스)
리스크: 운영 부담(서버·결제·CS·보안), 기존 도구(axe, Lighthouse)와 경쟁
→ "디자인 토큰 레벨 검사"로 차별화

#### ⑤ 웹 에디터 (비개발자용)
**난이도 ⭐⭐⭐☆☆ | 1~2개월**

색/폰트를 고르면 실시간 미리보기 + DESIGN.md·Tailwind·JSON 다운로드.

킬러 기능은 **AI 프로즈 자동생성**입니다.
사용자가 "성수동 편집샵 느낌"이라고 입력하면 `## Overview`와
`## Do's and Don'ts`를 AI가 작성. 대부분의 사람은 토큰은 고를 수 있어도
프로즈는 못 쓰기 때문에 여기에 가치가 있습니다.

React로 만들기 좋습니다: `js-yaml` + `remark` + `@google/design.md/linter` import.
AI 프로즈 기능 외에는 전부 브라우저에서 동작하므로 서버 비용이 없습니다.

가격: 무료(다운로드) / $5월(AI 프로즈 무제한 + 저장 + 팀공유)
여기서 ① 템플릿 팩을 크로스셀할 수 있습니다.

#### ⑥ 교육 콘텐츠 / 강의
**난이도 ⭐⭐☆☆☆ | 2~4주**

실제로 파는 건 DESIGN.md 사용법이 아니라 **"AI에게 의도를 정확히 전달하는 법"**입니다.
PHILOSOPHY.md의 원리는 디자인을 넘어 모든 프롬프팅에 적용되므로 대상이 넓습니다.

유튜브/블로그(무료 유입) → 전자책 ₩15,000~30,000 →
인프런/유데미 ₩50,000~150,000 → 기업 워크샵 ₩100~300만 → 유료 뉴스레터 $5월

①과 세트로 팔면 전환율이 좋습니다.

#### ⑦ 워드프레스 플러그인 (틈새)
**난이도 ⭐⭐⭐☆☆ | 1~2개월**

웹의 큰 비중을 차지하지만 AI 디자인 도구가 거의 없는 시장입니다.
DESIGN.md 업로드 → 테마 색/폰트 자동 반영 → 관리자 화면에서 가이드 확인.

재료: `symfony/yaml` + `league/commonmark`
**설계 팁:** 린터를 PHP로 다시 짜지 말고, PHP는 화면만 담당하고
검사는 `shell_exec('npx designmd lint ...')`로 JSON을 받으세요.

가격: WordPress.org 무료 배포 → Pro $39/년

### 8-3. 우선순위와 90일 로드맵

| 순위 | 아이디어 | 이유 |
|:--|:--|:--|
| 1 | ① 템플릿 | 즉시 시작 가능, 법적으로 가장 깨끗 |
| 2 | ② MCP | 직접수익은 낮지만 인지도가 나머지를 띄움 |
| 3 | ⑥ 교육 | ①과 세트 시너지 |
| 4 | ⑤ 에디터 | React 학습 겸 제작 |
| 5 | ③ Figma | 임팩트 크나 학습량 많음 |
| 6 | ④ SaaS | 수익 최대, 체력 필요 |
| 7 | ⑦ WP | 시장은 크나 결이 다름 |

```
Week 1-2    템플릿 3개 제작 + Gumroad 오픈 → 첫 매출로 검증
Week 3-6    MCP 서버 오픈소스 공개 → 개발자 유입, README에 템플릿 링크
Week 7-10   템플릿 8개로 확장 + 블로그/유튜브 → 트래픽↔매출 선순환
Week 11-12  반응에 따라 분기:
              개발자 유입이 많으면 → ⑤ 에디터
              기업 문의가 오면    → ④ SaaS
```

이유: ①은 검증이 빠르고(제작 3일, 결과 1주), ②는 무료지만 유입 엔진이며,
큰 투자(④)는 검증 이후에 들어가야 안전합니다.

### 8-4. 리스크

| 리스크 | 수준 | 대비책 |
|:--|:--|:--|
| 아직 alpha — 포맷 변경 가능 | 높음 | 템플릿은 텍스트 파일이라 수정이 쉬움 (①이 안전한 이유) |
| 스타 대비 실사용자 부족 가능성 | 높음 | 작게 검증 먼저, 크게 안 벌리기 |
| 구글이 직접 유료 기능 출시 | 중간 | 구글이 안 할 영역(한국 특화, 틈새) 공략 |
| 상표 문제 | 중간 | 구글 이름·로고 절대 사용 금지 (8-0 표 참고) |
| 포맷 자체가 확산 실패 | 중간 | 포맷 독립적으로 설계 |

**가장 중요한 원칙: DESIGN.md에 올인하지 말고, DESIGN.md를 통로로 쓸 것.**
내가 만든 색 조합·타이포 시스템·디자인 철학은 포맷이 사라져도 남습니다.
JSON으로도, Figma로도, Tailwind로도 팔 수 있는 자산입니다.

---

## 9. React / PHP로 만들 수 있는가?

**둘 다 가능합니다.** DESIGN.md는 텍스트 파일일 뿐이고,
읽는 데 필요한 건 YAML 파서와 마크다운 파서뿐이라 거의 모든 언어에 존재합니다.

### React (궁합 최상 ⭐⭐⭐⭐⭐)

| 만들 것 | 설명 |
|:--|:--|
| 웹 에디터 | 실시간 미리보기 + 다운로드 (8-2 ⑤) |
| DesignProvider | DESIGN.md → CSS 변수 주입, 테마 전환 |
| 스타일가이드 뷰어 | 파일 넣으면 문서 사이트 자동 생성 |
| 컴포넌트 프리뷰 | `components:` 토큰으로 실제 렌더링 |

```
브라우저: js-yaml + remark/marked → 파싱
검사:     import { lint } from '@google/design.md/linter'  ← 다시 안 짜도 됨
서버:     불필요 (AI 프로즈 기능 외)
```

### PHP (⭐⭐⭐)

잘 맞는 것: Laravel/워드프레스 테마 관리, 사내 디자인 포털, WP 플러그인
재료: `symfony/yaml` + `league/commonmark`

애매한 것: 린터를 PHP로 처음부터 재구현
(규칙 11개 + 색 대비 계산 + 토큰 참조 해석 → 노동량 크고 원본 추종이 어려움)

더 나은 방법: PHP는 화면만, 검사는 `shell_exec('npx designmd lint ...')`로 JSON 수신.

### 언어별 정리

| 언어 | 추천도 | 적합한 것 |
|:--|:--|:--|
| React | ⭐⭐⭐⭐⭐ | 에디터, 뷰어, 테마 시스템 |
| Node/TS | ⭐⭐⭐⭐⭐ | MCP 서버, CLI 확장 (원본이 TS) |
| PHP | ⭐⭐⭐ | 워드프레스/라라벨 연동 |

---

## 10. 다음 단계

| 코스 | 소요 | 내용 |
|:--|:--|:--|
| 맛보기 | 5분 | `bun install` 후 예제 lint 실행 |
| 실전 | 30분 | 내 프로젝트용 DESIGN.md 작성 (프로즈에 집중) |
| 주말 | 1~2일 | React 미니 에디터 제작 → ⑤/① 수익화로 연결 |
| 공부 | 반나절 | `.agents/skills/` 4개 분석 → 에이전트 설계 학습 |
| 사업 | 1주 | 템플릿 팩 1호 제작 + Gumroad 오픈 |

---

*이 노트는 저장소 소스코드를 직접 확인하여 작성되었습니다.*
*포맷 버전: `alpha` — 스펙 변경 가능성이 있으므로 최신 내용은 원본 저장소를 확인하세요.*
