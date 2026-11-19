---
name: 오늘의 타로
theme: dark
colors:
  midnight: "#0b0a14"
  velvet: "#15132a"
  nightshade: "linear-gradient(#1c1838, #0b0a14 288px)"
  hairline: "#2e2a4a"
  dusk: "#6f6a8c"
  mist: "#9a96b4"
  moonlight: "#f3f0fa"
  parchment: "#f4ecdc"
  ink: "#1d1a2e"
  candle-gold: "#d8b45a"
  candle-gold-active: "#c29d43"
  on-gold: "#1a1405"
  starlight: "#b9a6ff"
  ember: "#ff7a6b"
typography:
  display: { family: "Gowun Batang", substitute: "Noto Serif KR", weights: [400, 700] }
  text: { family: "Pretendard", substitute: "system-ui", weights: [400, 500, 600] }
rounded:
  tarot-card: 16px
  panel: 24px
  input: 14px
  toast: 20px
  pill: 9999px
spacing: [4, 8, 12, 16, 20, 24, 32, 48, 64]
components: [button, card, field, input, toggle-group, alert, badge, toast, drawer, separator, spinner]
---

# 오늘의 타로 — 디자인 가이드

> **한밤의 촛불 아래 카드 한 장.** 화면마다 어두운 벨벳 위에 카드 하나만 조명을 받고, 글씨와 버튼은 그 카드를 설명하는 조용한 라벨처럼 둘레에 놓입니다.

**Theme:** dark (MVP는 다크 모드 하나만 씁니다)

이 문서는 레퍼런스 DESIGN.md(어두운 무대 위 제품 한 개를 비추는 전시형 스타일)를 기획 문서 4개(`TARO_01_PRD` ~ `TARO_04_와이어프레임`)에 맞춰 다시 쓴 것입니다. 레퍼런스의 구조(검은 무대 · 절제된 강조색 · 큰 둥근 모서리 · 그림자 없는 층 구분)는 가져오고, 색 · 글꼴 · 크기는 **한국어 모바일 타로 서비스**에 맞게 바꿨습니다. 컴포넌트 규칙은 Tailwind CSS v4와 shadcn/ui 기준입니다.

## 1. 디자인 원칙

| # | 원칙 | 화면에서는 | 근거 |
|---|---|---|---|
| 1 | **카드가 주인공** | 한 화면에 조명받는 요소는 카드 하나. 나머지는 Mist · Moonlight 글씨와 작은 버튼 | PRD 해결 방안 |
| 2 | **금색은 한 화면에 한 번** | Candle Gold 채움 버튼은 화면당 1개 ([타로 시작] · [카드 한 장 뽑기]). 결과 화면에는 금색 버튼 없음 | F-1 · F-3 |
| 3 | **안심 문구는 늘 같은 자리** | 개인정보 안내는 입력칸 바로 아래(S-02), 버튼 묶음 아래(S-03)에 같은 모양으로 | 원칙 1 · F-2 · F-4 |
| 4 | **오락용임을 숨기지 않음** | 결과 카드 · 저장 이미지 · 공유 글 모두 "※ 오락용 타로 해석입니다" | 원칙 4 |
| 5 | **1분 안에 끝** | 스크롤 없이 한 화면(375×667 기준)에 주요 버튼까지 보이게 | PRD 제품 목표 |
| 6 | **그림자 대신 층** | 그림자 없이 Midnight → Velvet 바탕 차이와 1px 선으로 층을 나눔 | 레퍼런스 Elevation |

## 2. 색 (Colors)

| 이름 | 값 | 토큰 | 역할 |
|---|---|---|---|
| Midnight | `#0b0a14` | `--color-midnight` | 페이지 바탕, 카드 무대(S-01 · S-03 전체 배경) |
| Velvet | `#15132a` | `--color-velvet` | 패널 · 결과 카드 바탕, 보조 버튼 채움 |
| Nightshade | `linear-gradient(#1c1838, #0b0a14 288px)` | `--gradient-nightshade` | S-02 입력 화면 상단에서 아래로 번지는 바탕 (이 외 그라데이션 금지) |
| Hairline | `#2e2a4a` | `--color-hairline` | 카드 · 패널 1px 테두리, 구분선 |
| Dusk | `#6f6a8c` | `--color-dusk` | 입력칸 테두리, 외곽선 버튼 테두리, 비활성 글씨 |
| Mist | `#9a96b4` | `--color-mist` | 보조 설명, 개인정보 · 오락용 안내, 플레이스홀더 |
| Moonlight | `#f3f0fa` | `--color-moonlight` | 기본 글씨, 제목, 해석 본문 |
| Parchment | `#f4ecdc` | `--color-parchment` | 타로 카드 앞면 바탕(카드 그림 틀) |
| Ink | `#1d1a2e` | `--color-ink` | Parchment 위 글씨 · 선 (카드 번호 · 이름) |
| Candle Gold | `#d8b45a` | `--color-candle-gold` | 주요 행동 버튼 채움, 카드 뒷면 무늬 선, 별자리 기호 |
| Candle Gold Active | `#c29d43` | `--color-candle-gold-active` | 주요 버튼 누름 상태 |
| On Gold | `#1a1405` | `--color-on-gold` | 금색 버튼 위 글씨 |
| Starlight | `#b9a6ff` | `--color-starlight` | 링크, 포커스 링, 선택된 주제 칩 테두리 |
| Ember | `#ff7a6b` | `--color-ember` | 입력 오류("날짜를 다시 확인해 주세요")에만 |

### 대비 확인 (WCAG)

| 글씨 / 바탕 | 대비 | 용도 | 판정 |
|---|---|---|---|
| Moonlight / Midnight | 17.5:1 | 제목 · 본문 | AAA |
| Moonlight / Velvet | 16.1:1 | 결과 카드 해석 | AAA |
| Mist / Midnight | 6.9:1 | 안내 문구 12–14px | AA |
| Mist / Velvet | 6.4:1 | 결과 카드 안 오락용 안내 | AA |
| On Gold / Candle Gold | 9.2:1 | 주요 버튼 | AAA |
| Starlight / Midnight | 9.3:1 | 링크 · 포커스 | AAA |
| Ember / Midnight | 7.7:1 | 오류 문구 | AAA |
| Ink / Parchment | 14.4:1 | 카드 앞면 글씨 | AAA |

> Dusk(`#6f6a8c`)는 Midnight 위 대비가 3.9:1이라 **글씨 본문에 쓰지 않습니다.** 테두리와 비활성 표시에만 씁니다.

## 3. 글씨 (Typography)

| 글꼴 | 대체 글꼴 | 굵기 | 역할 |
|---|---|---|---|
| **Gowun Batang** (`--font-display`) | Noto Serif KR → serif | 400, 700 | 서비스 이름, 화면 제목, 카드 이름, 저장 이미지 제목. 촛불 아래 책 같은 느낌의 명조 |
| **Pretendard** (`--font-text`) | system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif | 400, 500, 600 | 본문, 해석, 버튼, 입력, 안내 문구 |

- 한국어는 `word-break: keep-all`, `line-break: strict`로 낱말 중간에서 줄이 바뀌지 않게 합니다.
- 숫자(생년월일 · 카드 번호)는 `font-variant-numeric: tabular-nums`.
- 카드 번호는 로마 숫자(0, I … XXI)를 Gowun Batang으로 씁니다.

### 글씨 크기 (Type Scale, 모바일 375px 기준)

| 역할 | 글꼴 | 굵기 | 크기 | 줄 간격 | 자간 | 토큰 / 유틸리티 | 쓰는 곳 |
|---|---|---|---|---|---|---|---|
| caption | Text | 400 | 12px | 1.5 | -0.1px | `type-caption` | 오락용 안내, 개인정보 안내 2줄째 |
| notice | Text | 400 | 13px | 1.55 | -0.15px | `type-notice` | 🔒 개인정보 안내, 입력 도움말 |
| label | Text | 500 | 14px | 1.43 | -0.2px | `type-label` | 입력 라벨, 주제 칩, 보조 버튼 |
| body | Text | 400 | 15px | 1.6 | -0.2px | `type-body` | 일반 본문, 시작 화면 소개 |
| button | Text | 600 | 16px | 1.25 | -0.2px | `type-button` | 주요 버튼 |
| reading | Text | 500 | 17px | 1.65 | -0.25px | `type-reading` | **해석 3줄** (결과 카드 핵심) |
| card-name | Display | 700 | 22px | 1.3 | 0 | `type-card-name` | "XIX 태양" |
| screen-title | Display | 700 | 24px | 1.3 | -0.2px | `type-screen-title` | "나에 대해 알려 주세요" |
| hero | Display | 700 | 36px | 1.2 | -0.5px | `type-hero` | S-01 "🔮 오늘의 타로" |

- 화면 너비 ≥ 768px에서는 `hero`만 44px로 키우고 나머지는 그대로 둡니다. 서비스 몸체는 최대 480px 폭 안에 있습니다.
- 해석 3줄(약 90자)은 `type-reading` 17px · 줄 간격 1.65로, 375px 폭에서 줄당 1문장이 들어가게 합니다.

## 4. 간격 · 모양 (Spacing & Shapes)

**밀도:** 여유 있게 (comfortable). 엄지로 누르는 모바일 화면입니다.

### 간격

| 이름 | 값 | Tailwind | 쓰는 곳 |
|---|---|---|---|
| 1 | 4px | `gap-1` | 아이콘 ↔ 글씨, 카드 이름 ↔ 별자리 |
| 2 | 8px | `gap-2` | 주제 칩 사이, 라벨 ↔ 입력칸 |
| 3 | 12px | `gap-3` | 버튼 2개 가로 사이, 해석 줄 묶음 안 |
| 4 | 16px | `px-4`, `p-4` | **화면 좌우 여백(고정)**, 카드 안쪽 여백 |
| 5 | 20px | `gap-5` | 입력 항목(Field) 사이 |
| 6 | 24px | `gap-6`, `p-6` | 섹션 사이, 결과 카드 안쪽 여백 |
| 8 | 32px | `gap-8` | 카드 그림 ↔ 해석 |
| 12 | 48px | `pt-12` | 화면 위 여백(S-01 제목 위) |
| 16 | 64px | `pb-16` | 화면 아래 안전 여백 + `env(safe-area-inset-bottom)` |

### 레이아웃

- 화면 좌우 여백 16px, 본문 최대 폭 480px 가운데 정렬. 가로 스크롤 없음.
- 주요 버튼은 화면 아래쪽 엄지 영역에 둡니다(S-01 · S-02).
- 세로 쌓기는 `flex flex-col gap-*`. `space-y-*`는 쓰지 않습니다.

### 둥근 모서리 (Border Radius)

| 요소 | 값 | Tailwind 클래스 (고정값) |
|---|---|---|
| 타로 카드 그림(앞 · 뒤) | 16px | `rounded-2xl` |
| 결과 카드 · 패널 · Drawer | 24px | `rounded-3xl` |
| 입력칸 | 14px | `rounded-lg` |
| 토스트 | 20px | `rounded-2xl`와 별도 `--radius-toast` |
| 버튼 · 주제 칩 · 배지 | 9999px | `rounded-full` / `rounded-4xl` |

### 크기 (터치 영역)

| 컨트롤 | 높이 | 가로 여백 |
|---|---|---|
| 주요 버튼 (`size="lg"`) | 52px | 24px, 폭 100% |
| 보조 버튼 (`size="default"`) | 48px | 20px |
| 작은 버튼 (`size="sm"`) | 40px | 16px |
| 입력칸 | 48px | 16px |
| 주제 칩 | 44px | 14px |
| 뒤로 가기 아이콘 버튼 (`size="icon"`) | 44×44px | — |

모든 누를 수 있는 요소는 44×44px 이상입니다.

## 5. 표면 · 층 (Surfaces & Elevation)

| 층 | 이름 | 값 | 쓰는 곳 |
|---|---|---|---|
| 0 | Midnight Stage | `#0b0a14` | 페이지 바탕, 카드 무대 |
| 1 | Velvet Panel | `#15132a` + 1px Hairline | 결과 카드, Drawer, 토스트 |
| 2 | Parchment Face | `#f4ecdc` | 타로 카드 앞면 그림 틀 (카드 안에서만) |

- **그림자는 쓰지 않습니다.** 층은 바탕색 차이와 1px Hairline(`#2e2a4a`) 선으로만 나눕니다.
- 유일한 빛 효과는 **Candle Glow**: 뽑힌 카드 뒤에만 깔리는 원형 빛
  `radial-gradient(closest-side, rgba(216,180,90,0.22), transparent)`.
  카드 무대(S-01 카드 뒷면, S-03 카드 그림) 외에는 쓰지 않습니다.

## 6. 그림 (Imagery)

- **카드 그림은 직접 만들었거나 사용 허가가 분명한 것만** 씁니다. (PRD 리스크 · 미정)
- 카드 비율 **3:5** (예: 화면 160×267px, 저장 이미지 432×720px). 앞면은 Parchment 바탕에 Ink 선, 위에 로마 숫자, 아래에 카드 이름.
- 카드 뒷면: Velvet 바탕 + Candle Gold 1px 선으로 그린 별 · 달 대칭 무늬. 모든 화면에서 같은 뒷면.
- 아이콘은 얇은 선 아이콘 한 종류(프로젝트의 shadcn `iconLibrary`)로 통일. 주제 칩의 이모지(💼💰💕🌿📚✨)와 🔮 · 🔒만 예외로 씁니다.
- 사람 사진, 실제 인물 얼굴, 별자리 사진은 쓰지 않습니다.

## 7. 움직임 (Motion)

| 이름 | 길이 | 곡선 | 쓰는 곳 |
|---|---|---|---|
| flip | 700ms | `cubic-bezier(0.2, 0.7, 0.2, 1)` | 카드 뒤집기(F-3, 1초 이내 조건) — `rotateY(180deg)` |
| glow-in | 400ms | ease-out | 카드가 뒤집힌 뒤 Candle Glow 나타나기 |
| rise | 250ms | ease-out | 해석 3줄이 아래에서 8px 올라오며 나타나기 (줄마다 80ms 차이) |
| toast | 200ms | ease-out | 토스트 나타나기 · 사라지기 |

- `prefers-reduced-motion: reduce`이면 뒤집기 · 올라오기를 끄고 150ms 페이드만 씁니다.
- 뒤집기 중에는 버튼을 누를 수 없게(`disabled`) 해서 두 번 뽑히지 않게 합니다.

## 8. 컴포넌트 (shadcn/ui 기준)

shadcn 규칙을 따릅니다: 색은 의미 토큰(`bg-primary`, `text-muted-foreground`)으로만, `className`은 배치에만, 아이콘은 `data-icon`, 세로 쌓기는 `gap-*`.

### 8-1. 화면 ↔ 컴포넌트 지도

| 화면 | 요소 | shadcn 컴포넌트 | 기능 |
|---|---|---|---|
| S-01 시작 | 서비스 이름 · 소개 | 글씨 (`type-hero`, `type-body`) | F-1 |
| | 카드 뒷면 그림 | 커스텀 `TarotCard` (뒷면) | F-1 |
| | [타로 시작] | `Button` `size="lg"` (default) | F-1 |
| | ※ 오락용 · 저장 안 해요 | `p.type-caption text-muted-foreground` | 원칙 1 · 4 |
| S-02 내 정보 | ← 뒤로 | `Button` `variant="ghost"` `size="icon"` + `aria-label="뒤로"` | F-2 |
| | 이름 · 생년월일 · 전공 | `FieldGroup` > `Field` > `FieldLabel` + `Input` + `FieldDescription` / `FieldError` | F-2 |
| | 주제 6개 | `FieldSet` + `FieldLegend` + `ToggleGroup` (단일 선택) | F-2 |
| | 🔒 개인정보 안내 | `Alert` (variant `notice`) | 원칙 1 |
| | [카드 한 장 뽑기] | `Button` `size="lg"`, 조건 전 `disabled` | F-2 · F-3 |
| S-03 결과 | 결과 카드 | `Card` (`CardHeader` · `CardContent` · `CardFooter`) | F-4 |
| | 카드 그림 | 커스텀 `TarotCard` (앞면, 뒤집기) | F-3 |
| | 별자리 · 주제 | `Badge` `variant="outline"` | F-4 |
| | [이미지 저장] · [결과 공유] | `Button` `variant="secondary"` + 아이콘 | F-5 · F-6 |
| | [다시 뽑기] · [처음으로] | `Button` `variant="outline"` / `variant="ghost"` | F-7 |
| | 저장 · 복사 결과 알림 | `toast` (Base UI) 또는 `sonner` (Radix) | F-5 · F-6 |
| | 길게 눌러 저장 · 복사 | `Drawer` + `DrawerTitle` | F-5 · F-6 |
| | 🔒 개인정보 안내 | `Alert` (variant `notice`) | 원칙 1 |

### 8-2. 버튼 (Button)

| variant | 바탕 | 글씨 | 테두리 | 쓰는 곳 | 한 화면 최대 |
|---|---|---|---|---|---|
| `default` | Candle Gold `bg-primary` | On Gold `text-primary-foreground` | 없음 | [타로 시작], [카드 한 장 뽑기] | **1개** |
| `secondary` | Velvet `bg-secondary` | Moonlight | 1px Hairline | [이미지 저장], [결과 공유] | 2개 |
| `outline` | 투명 | Moonlight | 1px Dusk `border-input` | [다시 뽑기] | — |
| `ghost` | 투명 (누르면 Velvet) | Mist → Moonlight | 없음 | [처음으로], ← 뒤로 | — |
| `link` | 투명 | Starlight | 밑줄 | 공유 글 미리보기 안 시작 링크 | — |

| 상태 | 규칙 |
|---|---|
| hover (데스크톱) | `default` → Candle Gold Active, 그 외 → `bg-accent` (Velvet) |
| active (누름) | `scale-[0.98]` + `default`는 Candle Gold Active |
| focus-visible | 2px Starlight 링, 2px 띄움 (`ring-2 ring-ring ring-offset-2 ring-offset-background`) |
| disabled | 투명도 40%, `pointer-events-none`. [카드 한 장 뽑기]는 이름 · 생년월일 · 주제가 다 차기 전까지 이 상태 |
| 처리 중 | `Button`에 `isLoading` 없음 → `<Spinner data-icon="inline-start" />` + `disabled` (이미지 만드는 중) |

- 모든 버튼은 **알약 모양(`rounded-full`)**. 네모 버튼은 쓰지 않습니다.
- 아이콘: `<DownloadIcon data-icon="inline-start" />이미지 저장`, `<Share2Icon data-icon="inline-start" />결과 공유`. 아이콘에 크기 클래스를 붙이지 않습니다.
- 버튼 글씨는 동사로 끝나는 짧은 말: "타로 시작", "카드 한 장 뽑기", "이미지 저장", "결과 공유", "다시 뽑기", "처음으로".

```tsx
<Button size="lg" className="w-full" disabled={!canDraw}>카드 한 장 뽑기</Button>

<div className="grid grid-cols-2 gap-3">
  <Button variant="secondary"><DownloadIcon data-icon="inline-start" />이미지 저장</Button>
  <Button variant="secondary"><Share2Icon data-icon="inline-start" />결과 공유</Button>
  <Button variant="outline">다시 뽑기</Button>
  <Button variant="ghost">처음으로</Button>
</div>
```

### 8-3. 결과 카드 (Card) — S-03 · 저장 이미지 영역

- 바탕 Velvet `bg-card`, 1px Hairline, 모서리 24px, 안쪽 여백 24px, **그림자 없음**.
- 반드시 `CardHeader` / `CardTitle` / `CardContent` / `CardFooter`로 나눕니다.

| 칸 | 내용 | 스타일 |
|---|---|---|
| `CardHeader` | `CardTitle` "지민님의 타로" + `Badge` "커리어" | `type-label`, Moonlight |
| `CardContent` 1 | `TarotCard` 앞면 (160×267px, 가운데) + Candle Glow | 뒤집기 효과 |
| `CardContent` 2 | "XIX 태양" + `Badge` "♌ 사자자리" | `type-card-name` + Badge 안 별자리 기호 Candle Gold |
| `CardContent` 3 | 해석 3줄 (각 줄 `<p>`) | `type-reading`, Moonlight, 줄 사이 `gap-1` |
| `CardFooter` | ※ 오락용 타로 해석입니다 | `type-caption`, Mist |

- 이 `Card` 하나가 그대로 저장 이미지(F-5)가 됩니다. 카드 안에 버튼을 넣지 않습니다.
- 생년월일 · 전공 원문은 카드에 쓰지 않습니다(원칙 2). 전공은 해석 3줄째 문장에만 녹아 있습니다.

### 8-4. 입력 (Field · Input) — S-02

```tsx
<FieldGroup>
  <Field>
    <FieldLabel htmlFor="name">이름 (닉네임 OK)</FieldLabel>
    <Input id="name" maxLength={10} autoComplete="off" placeholder="지민" />
    <FieldDescription>결과 이미지와 공유 글에 이 이름이 들어가요</FieldDescription>
  </Field>
  <Field data-invalid={birthError || undefined}>
    <FieldLabel htmlFor="birth">생년월일</FieldLabel>
    <Input id="birth" inputMode="numeric" placeholder="2004.08.03" aria-invalid={birthError || undefined} />
    {birthError && <FieldError>날짜를 다시 확인해 주세요</FieldError>}
  </Field>
  <Field>
    <FieldLabel htmlFor="major">전공 (선택)</FieldLabel>
    <Input id="major" autoComplete="off" placeholder="경영학과" />
  </Field>
</FieldGroup>
```

| 항목 | 규칙 |
|---|---|
| 바탕 · 테두리 | `rgba(255,255,255,0.04)` 바탕, 1px Dusk(`border-input`), 모서리 14px, 높이 48px |
| 글씨 | 16px Pretendard Moonlight (16px 미만이면 iOS가 확대하므로 16px 고정), 플레이스홀더 Mist |
| focus | 테두리 Starlight + 2px Starlight 링 |
| 오류 | `Field`에 `data-invalid`, `Input`에 `aria-invalid` → 테두리 Ember, `FieldError` Ember 13px |
| 생년월일 | 숫자 8자리 입력 시 `YYYY.MM.DD`로 자동 점 찍기. 실제 없는 날짜(2월 30일 등) · 미래 날짜는 오류 |
| 자동 저장 막기 | 모든 입력에 `autoComplete="off"`, 브라우저 저장소에 쓰지 않음 (기능명세서 데이터 표) |
| 이름 안내 | `FieldDescription`으로 "결과 이미지와 공유 글에 이 이름이 들어가요" (PRD 리스크: 실명 퍼짐) |

### 8-5. 주제 선택 (ToggleGroup) — S-02

- 6개 중 하나 → shadcn 규칙대로 `ToggleGroup` 단일 선택. `Button`을 반복하며 직접 선택 상태를 만들지 않습니다.
- `FieldSet` + `FieldLegend` "어떤 주제가 궁금한가요?"로 묶습니다.
- 3열 × 2줄 그리드(`grid grid-cols-3 gap-2`), 칩 높이 44px, 알약 모양.

| 상태 | 바탕 | 글씨 | 테두리 |
|---|---|---|---|
| 기본 | Velvet | Moonlight | 1px Hairline |
| 선택됨 (`data-state="on"` / `aria-pressed`) | `rgba(185,166,255,0.14)` | Moonlight 600 | 1px Starlight |
| focus-visible | — | — | 2px Starlight 링 |

순서는 고정: 💼 커리어 · 💰 재물 · 💕 연애 · 🌿 건강 · 📚 학업 · ✨ 종합.

### 8-6. 개인정보 안내 (Alert, variant `notice`)

- 직접 꾸민 `div`가 아니라 `Alert`에 `notice` variant를 하나 더해서 씁니다.
- 바탕 투명, 1px Hairline, 모서리 14px, 안쪽 여백 12px, 아이콘 🔒 또는 `LockIcon`, 글씨 `type-notice` Mist.
- 문구는 기능명세서 그대로 쓰고, 화면마다 바꾸지 않습니다.
  - S-02 (입력칸 바로 아래): "입력한 정보는 해석을 만드는 데만 쓰고 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요."
  - S-03 (버튼 묶음 아래): "정보는 저장되지 않아요. [처음으로]를 누르면 바로 지워져요."

### 8-7. 배지 (Badge)

| 쓰는 곳 | variant | 모양 |
|---|---|---|
| 주제 ("커리어") | `outline` | 1px Hairline, Moonlight 12px 500, 알약 |
| 별자리 ("♌ 사자자리") | `outline` | 기호만 Candle Gold, 글씨 Moonlight |

색만으로 뜻을 나타내지 않고, 배지 안에는 항상 글씨가 있습니다.

### 8-8. 알림 (Toast) · 대체 화면 (Drawer) — F-5 · F-6

| 상황 (기능명세서) | 컴포넌트 | 문구 |
|---|---|---|
| 이미지 저장 성공 | `toast` | 이미지를 저장했어요 |
| 이미지 저장 안 됨 | `Drawer` — 이미지 + 안내 | 이미지를 길게 눌러 저장해 주세요 |
| 공유 메뉴 열림 / 취소 | 없음 | (결과 화면 그대로) |
| 공유 메뉴 없음 → 복사 성공 | `toast` | 결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요 |
| 복사도 실패 | `Drawer` — 공유 글 + 안내 | 아래 글을 길게 눌러 복사해 주세요 |

- 토스트: Velvet 바탕, 1px Hairline, 모서리 20px, 화면 아래 가운데, 2.5초 뒤 사라짐, 오류색 없음(실패도 다음 행동을 알려 주는 안내라서).
- Drawer: 아래에서 올라오는 시트, 모서리 위쪽 24px, `DrawerTitle` 필수(보이지 않게 하려면 `sr-only`), 안의 이미지 · 글은 `user-select: text`, `-webkit-touch-callout: default`로 길게 눌러 저장 · 복사가 되게.
- Base UI 프로젝트는 `toast.add({ title })`, Radix 프로젝트는 `sonner`의 `toast()`.

### 8-9. 타로 카드 (커스텀 `TarotCard`)

shadcn에 없는 유일한 커스텀 컴포넌트입니다.

| 속성 | 값 |
|---|---|
| 크기 | 화면 160×267px (3:5), 저장 이미지 432×720px |
| 모서리 | 16px, 테두리 1px Candle Gold 40% |
| 뒷면 | Velvet + Candle Gold 무늬 |
| 앞면 | Parchment 바탕, 위 로마 숫자, 가운데 그림, 아래 카드 이름(Ink, Gowun Batang) |
| 뒤집기 | `perspective: 1000px`, `transform-style: preserve-3d`, `backface-visibility: hidden`, 700ms |
| 접근성 | `role="img"`, `aria-label="XIX 태양 카드"`. 뒤집기가 끝나면 해석 영역에 `aria-live="polite"` |
| 방향 | 정방향만 (역방향 없음 — MVP 범위) |

## 9. 저장 이미지 (1080×1350, F-5)

S-03의 결과 `Card`를 그대로 3배로 키운 세로 이미지입니다.

| 영역 | 값 |
|---|---|
| 바탕 | Midnight 전체 + 가운데 Candle Glow |
| 안쪽 여백 | 좌우 72px, 위 96px, 아래 72px |
| 제목 | "지민님의 타로 · 커리어" Gowun Batang 44px Moonlight |
| 카드 그림 | 432×720px, 가운데 |
| 카드 이름 · 별자리 | "XIX 태양 · ♌ 사자자리" Gowun Batang 56px (별자리 기호 Candle Gold) |
| 해석 3줄 | Pretendard 500 44px, 줄 간격 1.55, Moonlight |
| 오락용 안내 | Pretendard 32px Mist |
| 맨 아래 | 서비스 이름 "🔮 오늘의 타로" Gowun Batang 32px Candle Gold |
| 넣지 않는 것 | 생년월일, 전공 원문, 버튼, 개인정보 안내 |

## 10. 문구 톤

- 해요체로, 짧게. "~할 때예요", "~돌아볼 때예요".
- 건강 · 재물은 단정하지 않습니다. ✕ "돈을 벌게 됩니다" → ○ "지출 우선순위를 돌아볼 때예요".
- 해석 첫 줄은 "{이름}님,"으로 시작합니다.
- 숫자 · 날짜는 `2004.08.03` 형식.

## 11. Do's and Don'ts

### Do

- 페이지 바탕은 Midnight `#0b0a14`, 패널 · 결과 카드는 Velvet `#15132a`.
- 제목 · 해석은 Moonlight `#f3f0fa`, 안내 · 보조 글씨는 Mist `#9a96b4`.
- Candle Gold `#d8b45a` 채움 버튼은 [타로 시작] · [카드 한 장 뽑기]에만, 화면당 한 개.
- 버튼 · 칩은 알약 모양, 카드 · 패널은 24px, 카드 그림은 16px 모서리.
- 개인정보 안내는 `Alert` notice로 S-02 입력칸 바로 아래, S-03 버튼 아래에 같은 문구로.
- 결과 카드 · 저장 이미지 · 공유 글에 "※ 오락용 타로 해석입니다".
- 주제 선택은 `ToggleGroup`, 입력은 `FieldGroup` + `Field`, 결과는 `Card` 전체 구성.
- 모든 터치 영역 44px 이상, 입력 글씨 16px 이상.

### Don't

- 그림자(`shadow-*`)를 쓰지 않습니다. Candle Glow는 카드 뒤에만.
- Nightshade(S-02 바탕)와 Candle Glow 외의 그라데이션을 만들지 않습니다.
- Candle Gold를 넓은 바탕 · 카드 채움 · 오류 표시에 쓰지 않습니다.
- Ember를 오류 외(강조, 버튼, 제목)에 쓰지 않습니다.
- 흰색 `#ffffff`을 기본 글씨로 쓰지 않습니다. Moonlight를 씁니다.
- Dusk를 본문 글씨에 쓰지 않습니다(대비 부족).
- 결과 카드 · 저장 이미지 · 공유 글에 생년월일이나 전공 원문을 넣지 않습니다.
- `space-y-*`, 직접 쓴 `dark:` 색, `bg-[#...]` 같은 날 값 색을 컴포넌트에 쓰지 않습니다.
- 네모 버튼, 12px 미만 글씨, 한 화면에 금색 버튼 두 개를 쓰지 않습니다.

## 12. Tailwind v4 · shadcn 테마 (globals.css)

shadcn의 `tailwindCssFile`에만 넣습니다. MVP는 다크 하나라서 `:root`와 `.dark`에 같은 값을 둡니다. hex 값은 그대로 씁니다.

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:where(.dark, .dark *));

:root {
  /* shadcn 의미 토큰 → 타로 색 */
  --background: #0b0a14;          /* Midnight */
  --foreground: #f3f0fa;          /* Moonlight */
  --card: #15132a;                /* Velvet */
  --card-foreground: #f3f0fa;
  --popover: #15132a;
  --popover-foreground: #f3f0fa;
  --primary: #d8b45a;             /* Candle Gold */
  --primary-foreground: #1a1405;  /* On Gold */
  --primary-active: #c29d43;      /* Candle Gold Active */
  --secondary: #15132a;           /* Velvet */
  --secondary-foreground: #f3f0fa;
  --muted: #15132a;
  --muted-foreground: #9a96b4;    /* Mist */
  --accent: #1f1c38;              /* ghost hover, 칩 hover */
  --accent-foreground: #f3f0fa;
  --destructive: #ff7a6b;         /* Ember — 입력 오류만 */
  --border: #2e2a4a;              /* Hairline */
  --input: #6f6a8c;               /* Dusk */
  --ring: #b9a6ff;                /* Starlight */

  /* 이름 있는 타로 토큰 */
  --parchment: #f4ecdc;
  --ink: #1d1a2e;
  --starlight: #b9a6ff;
  --selected: rgba(185, 166, 255, 0.14);
  --field: rgba(255, 255, 255, 0.04);
  --gradient-nightshade: linear-gradient(#1c1838, #0b0a14 288px);
  --candle-glow: radial-gradient(closest-side, rgba(216, 180, 90, 0.22), transparent);
}

.dark {
  /* MVP는 :root와 같음. 라이트 모드를 만들 때 :root를 바꾸고 여기에 다크 값을 남깁니다. */
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-primary-active: var(--primary-active);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-parchment: var(--parchment);
  --color-ink: var(--ink);
  --color-starlight: var(--starlight);
  --color-selected: var(--selected);
  --color-field: var(--field);

  /* 글꼴 */
  --font-display: "Gowun Batang", "Noto Serif KR", serif;
  --font-sans: "Pretendard", system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;

  /* 둥근 모서리 — 컴포넌트가 쓰는 클래스에 고정 */
  --radius-sm: 6px;       /* 작은 표시 */
  --radius-md: 10px;      /* 메뉴 항목 */
  --radius-lg: 14px;      /* 입력칸, 개인정보 Alert */
  --radius-xl: 24px;      /* Card, Drawer */
  --radius-2xl: 16px;     /* TarotCard 그림 */
  --radius-3xl: 24px;     /* 결과 패널 */
  --radius-4xl: 9999px;   /* Badge, 칩 */
  --radius-toast: 20px;
}

@theme {
  /* 그림자 없음 — 테두리로만 층 구분 */
  --shadow-xs: 0 0 #0000;
  --shadow-sm: 0 0 #0000;
  --shadow-md: 0 0 #0000;
  --shadow-lg: 0 0 #0000;

  /* 움직임 */
  --animate-flip: flip 700ms cubic-bezier(0.2, 0.7, 0.2, 1) both;
  --animate-glow-in: glow-in 400ms ease-out both;
  --animate-rise: rise 250ms ease-out both;

  @keyframes flip {
    from { transform: rotateY(0deg); }
    to { transform: rotateY(180deg); }
  }
  @keyframes glow-in {
    from { opacity: 0; transform: scale(0.8); }
    to { opacity: 1; transform: scale(1); }
  }
  @keyframes rise {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }
}

/* 글씨 크기 유틸리티 */
@utility type-caption { font-size: 12px; line-height: 1.5; letter-spacing: -0.1px; }
@utility type-notice { font-size: 13px; line-height: 1.55; letter-spacing: -0.15px; }
@utility type-label { font-size: 14px; line-height: 1.43; letter-spacing: -0.2px; font-weight: 500; }
@utility type-body { font-size: 15px; line-height: 1.6; letter-spacing: -0.2px; }
@utility type-button { font-size: 16px; line-height: 1.25; letter-spacing: -0.2px; font-weight: 600; }
@utility type-reading { font-size: 17px; line-height: 1.65; letter-spacing: -0.25px; font-weight: 500; }
@utility type-card-name { font-family: var(--font-display); font-size: 22px; line-height: 1.3; font-weight: 700; }
@utility type-screen-title { font-family: var(--font-display); font-size: 24px; line-height: 1.3; letter-spacing: -0.2px; font-weight: 700; }
@utility type-hero { font-family: var(--font-display); font-size: 36px; line-height: 1.2; letter-spacing: -0.5px; font-weight: 700; }

@layer base {
  * { @apply border-border outline-ring/50; }
  html { color-scheme: dark; }
  body {
    @apply bg-background text-foreground font-sans antialiased;
    word-break: keep-all;
    line-break: strict;
  }
  input { font-size: 16px; }
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
      animation-duration: 150ms !important;
      animation-name: fade-in !important;
      transition-duration: 150ms !important;
    }
  }
  @keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
}
```

### shadcn 시작 방법

- 스타일: **`luma`** — 알약 버튼, 둥근 모서리, 여유 있는 간격이 이 가이드와 가장 가깝습니다.
- 처음 만들 때: `npx shadcn@latest init --base base --preset luma --template vite --name taro --no-monorepo -y`
- 필요한 컴포넌트: `npx shadcn@latest add button card field input toggle-group alert badge toast drawer separator spinner`
- 버튼 높이(52 / 48 / 40px)와 입력 높이(48px)는 `button.tsx` · `input.tsx`의 `cva` size 값을 함께 바꿉니다.
- `Alert`에 `notice` variant를 `cva`로 하나 더합니다(바탕 투명, Hairline 테두리, Mist 글씨).

## 13. 미정 (Known Gaps)

- 카드 그림 22장 출처와 그림 스타일 (PRD 미정) — 정해지면 6장 그림 규칙을 업데이트합니다.
- Gowun Batang · Pretendard 웹폰트 용량: 저장 이미지(canvas)에 글꼴이 들어가려면 미리 불러와야 합니다.
- 라이트 모드: MVP에서 만들지 않음.
- 개인정보 동의 체크박스가 필요해지면 S-02에 `Field` + `Checkbox` 규칙을 더합니다.
- 주제를 3개로 줄이면 `ToggleGroup`을 3열 1줄로 바꿉니다.
