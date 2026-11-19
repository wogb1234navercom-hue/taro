---
name: 오늘의 타로
version: 2
source: 명지대학교 타로 디자인 팩.fig (선배 디자인 시스템, 2026-11-07)
theme: light
colors:
  bg: "#f3f3f5"
  surface: "#ffffff"
  surface-sub: "#f6f6f8"
  text-primary: "#000000"
  text-secondary: "#4d4d4e"
  text-tertiary: "#676e6a"     # 팩 값 #979f9b → 글씨 대비 때문에 진하게
  text-on-accent: "#000000"    # 팩 값 #ffffff → 대비 때문에 검정
  border: "#dcdcdd"
  accent: "#00d959"
  accent-soft: "#e6faef"
  accent-strong: "#007a37"     # 팩 값 #00d959 → 글씨용이라 진하게
  accent-illust: "#00de00"
  disabled: "#d7d7d7"
  danger: "#c9353b"            # 팩 값 #e5484d → 13px 글씨 대비 때문에 진하게
  inverse: "#232427"
typography:
  family: "Noto Sans KR"
  tracking: "-2%"
rounded:
  tarot-card: 10px
  tarot-card-back: 12px
  input: 12px
  notice: 12px
  toast: 12px
  button-m: 14px
  button-l: 16px
  chip: 22px
  card: 24px
spacing: [2, 6, 8, 10, 11, 12, 14, 16, 20, 24, 28, 34, 44]
components: [app-bar, button, topic-chip, input, privacy-notice, toast, tarot-card, result-card, card-deck]
---

# 오늘의 타로 — 디자인 가이드 v2

> **밝은 책상 위에 펼친 카드 한 벌.** 연회색 바탕 위에 흰 둥근 카드가 놓이고, 연두색은 "지금 누를 것"과 "고른 것"에만 씁니다. 카드 그림은 진짜 타로(Rider-Waite-Smith, 1909)를 그대로 보여 줍니다.

**Theme:** light (MVP는 라이트 모드 하나만 씁니다)

이 문서는 선배가 준 디자인 시스템 파일 **`명지대학교 타로 디자인 팩.fig`**(변수 15개 · 글씨 스타일 8개 · 컴포넌트 9종 · 카드 22장 · 와이어프레임 9화면 · 디자인 가이드 7장)를 기준으로 v1(어두운 촛불 테마)을 바꿔 쓴 것입니다. 기획 문서 4개(`TARO_01` ~ `TARO_04`)와 맞춰 두었고, 컴포넌트 규칙은 Tailwind CSS v4 · shadcn/ui 기준입니다.

### v1 → v2에서 바뀐 것

| 항목 | v1 | v2 (디자인 팩) |
|---|---|---|
| 테마 | 다크 (Midnight · Candle Gold) | **라이트** (연회색 #F3F3F5 · 흰 카드 · 연두 #00D959) |
| 글꼴 | Gowun Batang + Pretendard | **Noto Sans KR 하나**, 자간 -2% |
| 버튼 | 알약 모양 | **둥근 사각형** (L 16px · M 14px) |
| 카드 그림 | 직접 그린 임시 그림 | **Rider-Waite-Smith(1909) 22장** 실제 그림 |
| 카드 뽑기 | 버튼 → 바로 뒤집기 | **22장 부채꼴 덱 → 스와이프 → 탭 → 가운데로 → 뒤집기** (S-03-P · S-03-D 새 화면) |
| 그림자 | 없음 (Candle Glow만) | 카드 앞면 그림자 1종 + 고른 카드 연두 빛 1종 |
| 결과 화면 주요 버튼 | 없음 (금색 없음) | **[결과 공유]만 Primary** |

### 디자인 팩에서 바꾼 값 (접근성)

팩의 색 가운데 글씨에 쓰이는 4개는 WCAG 대비 기준을 넘지 못해, **글씨에 쓸 때만** 진한 값으로 바꿨습니다. 배경 · 테두리 · 버튼 채움 색은 팩 값 그대로입니다. (2026-11-19 결정)

| 토큰 | 팩 값 | 대비 | v2 값 | 대비 | 쓰는 곳 |
|---|---|---|---|---|---|
| text/on-accent | `#FFFFFF` | 1.9:1 (on #00D959) | `#000000` | 11.1:1 | Primary 버튼 글씨 |
| accent-strong | `#00D959` | 1.9:1 (on 흰색) | `#007A37` | 5.5:1 | 카드 이름 줄, 선택된 주제 칩 글씨 |
| text/tertiary | `#979F9B` | 2.5:1 (on #F3F3F5) | `#676E6A` | 4.7:1 | 오락용 안내, 플레이스홀더, 보조 설명 |
| danger | `#E5484D` | 3.9:1 (on 흰색) | `#C9353B` | 5.2:1 | 입력 오류 테두리 · 문구 |

## 1. 디자인 원칙

| # | 원칙 | 화면에서는 | 근거 |
|---|---|---|---|
| 1 | **카드가 주인공** | 카드 그림만 그림자를 갖고, 나머지는 평평한 흰 면과 1px 선 | PRD 해결 방안 |
| 2 | **연두는 "누를 것 · 고른 것"에만** | Primary 버튼 화면당 1개, 선택된 칩, 덱 카드 테두리, 스와이프 안내 | 팩 03 Button |
| 3 | **안심 문구는 늘 같은 자리** | Privacy Notice를 S-02 입력칸 아래 · S-03 버튼 아래에 같은 문구로 | 원칙 1 · F-2 · F-4 |
| 4 | **오락용임을 숨기지 않음** | 결과 카드 · 저장 이미지 · 공유 글에 "※ 오락용 타로 해석입니다" | 원칙 4 |
| 5 | **고르는 재미, 1분 안에 끝** | 덱을 넘기고 고르는 동작은 넣되, 각 움직임은 0.6초 이하 | PRD 제품 목표 · 팩 05 |

## 2. 색 (Colors)

| 이름 | 값 | 토큰 | 역할 |
|---|---|---|---|
| bg | `#F3F3F5` | `--color-bg` | 화면 바탕 (모든 화면) |
| surface | `#FFFFFF` | `--color-surface` | 결과 카드, 입력칸, 칩 기본, Secondary 버튼 |
| surface-sub | `#F6F6F8` | `--color-surface-sub` | Privacy Notice 바탕 |
| text/primary | `#000000` | `--color-text-primary` | 제목, 입력값, 해석 본문 |
| text/secondary | `#4D4D4E` | `--color-text-secondary` | 입력 라벨, 칩 기본 글씨, 안내 본문, 시작 화면 소개 |
| text/tertiary | `#676E6A` | `--color-text-tertiary` | 오락용 안내, 플레이스홀더, 동작 설명 캡션 |
| text/on-accent | `#000000` | `--color-text-on-accent` | Primary 버튼 글씨 |
| border | `#DCDCDD` | `--color-border` | 입력칸 · Secondary 버튼 · 칩 테두리 |
| accent | `#00D959` | `--color-accent` | Primary 버튼 채움, 포커스 테두리, 선택 칩 테두리, 카드 뒷면 테두리 |
| accent-soft | `#E6FAEF` | `--color-accent-soft` | 선택된 칩 바탕, 카드 뒷면 원 |
| accent-strong | `#007A37` | `--color-accent-strong` | 연두 계열 **글씨** (카드 이름 줄, 선택된 칩 글씨) |
| accent-illust | `#00DE00` | `--color-accent-illust` | 스와이프 안내 화살표 · "Swipe!" (장식, 18px Bold) |
| disabled | `#D7D7D7` | `--color-disabled` | 비활성 버튼 채움 |
| danger | `#C9353B` | `--color-danger` | 입력 오류 테두리 · 문구만 |
| inverse | `#232427` | `--color-inverse` | 토스트 바탕 |

### 대비 확인 (WCAG)

| 글씨 / 바탕 | 대비 | 용도 | 판정 |
|---|---|---|---|
| text/primary / bg | 19.0:1 | 제목 · 본문 | AAA |
| text/secondary / surface | 8.4:1 | 라벨 · 안내 | AAA |
| text/secondary / surface-sub | 7.8:1 | Privacy Notice | AAA |
| text/tertiary / bg | 4.7:1 | 캡션 | AA |
| text/on-accent / accent | 11.1:1 | Primary 버튼 | AAA |
| accent-strong / surface | 5.5:1 | 카드 이름 줄 | AA |
| accent-strong / accent-soft | 5.0:1 | 선택된 칩 글씨 | AA |
| danger / surface | 5.2:1 | 오류 문구 | AA |
| 흰 글씨 / inverse | 15.5:1 | 토스트 | AAA |
| 흰 글씨 / disabled | 1.4:1 | 비활성 버튼 | WCAG 예외(비활성) — 글씨 대신 상태로 전달 |

> accent-illust `#00DE00`은 흰 바탕 대비가 낮아 **장식용**입니다. "Swipe!" 옆에 항상 text/tertiary 설명("좌우로 넘기고, 끌리는 카드를 탭하세요")을 함께 둡니다.

## 3. 글씨 (Typography)

**Noto Sans KR** 하나만 씁니다. 모든 스타일의 자간은 **-2%**입니다. 한국어는 `word-break: keep-all`.

| 스타일 | 굵기 | 크기 / 줄 높이 | 토큰 / 유틸리티 | 쓰는 곳 |
|---|---|---|---|---|
| Display | Bold | 28 / 38 | `type-display` | S-01 "오늘의 타로" |
| Title | Bold | 22 / 32 | `type-title` | 화면 질문 ("어떤 주제가 궁금한가요?", "커리어를 떠올리며 카드 한 장을 골라 주세요", "XIX 태양이 나왔어요") |
| Headline | Bold | 18 / 26 | `type-headline` | 앱바 제목, 카드 이름 줄 ("XIX 태양 · 사자자리"), "Swipe!" |
| Body | Regular | 16 / 26 | `type-body` | 해석 본문(가운데 정렬, 3줄 · 90자 이내), 입력값, 시작 화면 소개 |
| Body Bold | Bold | 16 / 24 | `type-body-bold` | L 버튼 |
| Label | Medium | 15 / 22 | `type-label` | M 버튼, 주제 칩, 토스트 |
| Caption | Regular | 13 / 19 | `type-caption` | 안내 · 보조 · 오락용 안내 · 오류 문구 |
| Caption Bold | Bold | 13 / 19 | `type-caption-bold` | 입력 라벨, 결과 카드 제목 ("지민님의 타로 · 커리어") |

- 숫자(생년월일 · 카드 번호)는 `font-variant-numeric: tabular-nums`.
- 카드 번호는 로마 숫자(0, I … XXI) + 한글 이름: "XIX 태양".
- 입력값은 16px이라 iOS에서 확대되지 않습니다.

## 4. 간격 · 모양 (Spacing & Shapes)

### 화면 틀 (375 × 812)

| 영역 | 값 |
|---|---|
| 위 안전 영역 | 44px (상태 표시줄) |
| 앱바 | 높이 56px, 좌우 16px |
| 본문 좌우 여백 | **20px** → 콘텐츠 폭 335px |
| 아래 안전 영역 | 34px (+ `env(safe-area-inset-bottom)`) |
| 하단 CTA 영역 | 위 12px · 좌우 20px · 아래 34px, 화면 아래 고정 |

### 간격

| 값 | 쓰는 곳 |
|---|---|
| 2px | 해석 줄 사이 |
| 6px | 버튼 아이콘 ↔ 라벨 |
| 8px | 입력 라벨 ↔ 입력칸 ↔ 도움말, 앱바 요소 사이 |
| 10px | 주제 칩 사이(가로 · 세로), Notice 아이콘 ↔ 글 |
| 11px | 결과 화면 M 버튼 2개 사이 (162 + 11 + 162 = 335) |
| 14px | 결과 화면 본문 요소 사이 |
| 16px | 입력 항목 사이, 결과 카드 안 요소 사이 |
| 20px | 화면 좌우 여백, 카드 공개 화면 요소 사이 |
| 24px | 시작 화면 요소 사이, 결과 카드 좌우 안쪽 여백 |
| 28px | 결과 카드 위아래 안쪽 여백 |

세로 쌓기는 `flex flex-col gap-*`. `space-y-*`는 쓰지 않습니다.

### 둥근 모서리

| 요소 | 값 | Tailwind (고정값) |
|---|---|---|
| 타로 카드 앞면 | 10px | `rounded-[10px]` → `--radius-tarot` |
| 타로 카드 뒷면 | 12px (안쪽 선 8px) | `--radius-tarot-back` |
| 입력칸 · Notice · 토스트 | 12px | `rounded-lg` |
| M 버튼 | 14px | `rounded-xl` |
| L 버튼 | 16px | `rounded-2xl` |
| 주제 칩 | 22px (높이 44의 절반 = 알약) | `rounded-full` |
| 결과 카드 | 24px | `rounded-3xl` |

### 크기 (터치 영역)

| 컨트롤 | 크기 |
|---|---|
| L 버튼 | 335 × 56 |
| M 버튼 | 162 × 48 |
| 입력칸 | 335 × 52 |
| 주제 칩 | 105 × 44 |
| 앱바 뒤로 가기 | 아이콘 20px, 누르는 영역 44 × 44 |
| 덱 카드 (S-03-P) | 108 × 180 |

## 5. 표면 · 그림자 (Surfaces & Elevation)

| 층 | 이름 | 값 | 쓰는 곳 |
|---|---|---|---|
| 0 | bg | `#F3F3F5` | 화면 바탕 |
| 1 | surface | `#FFFFFF` (+ 필요하면 1px border) | 결과 카드, 입력칸, 칩, Secondary 버튼 |
| 1 | surface-sub | `#F6F6F8` | Privacy Notice |
| 2 | inverse | `#232427` | 토스트 |

| 그림자 | 값 | 쓰는 곳 |
|---|---|---|
| card | `0 6px 16px rgba(0,0,0,0.12)` | 타로 카드 앞면만 |
| picked | `0 10px 28px rgba(0,217,89,0.35)` | 고른 카드가 가운데로 올라왔을 때(S-03-P2)만 |

그 밖의 요소(버튼 · 결과 카드 · 입력칸)에는 그림자를 쓰지 않습니다.

## 6. 카드 그림 (Imagery)

- **Rider-Waite-Smith(1909) 메이저 아르카나 22장** 그림을 씁니다. 1909년 출판본으로 저작권이 끝난(퍼블릭 도메인) 그림입니다. 디자인 팩의 `Tarot Deck · Major Arcana` 컴포넌트 22개(`Tarot Card / 00 The Fool` … `21 The World`)에 들어 있습니다.
- 원본 그림은 500 × 836px JPEG. 카드 앞면 비율은 **160 : 268**(약 3 : 5). 그림 위에 글씨를 올리지 않습니다(카드에 이미 번호 · 이름이 인쇄되어 있음).
- 화면에 쓰는 한글 이름은 카드 아래 따로 씁니다: 0 바보 · I 마법사 · II 여사제 · III 여황제 · IV 황제 · V 교황 · VI 연인 · VII 전차 · VIII 힘 · IX 은둔자 · X 운명의 수레바퀴 · XI 정의 · XII 매달린 사람 · XIII 죽음 · XIV 절제 · XV 악마 · XVI 탑 · XVII 별 · XVIII 달 · XIX 태양 · XX 심판 · XXI 세계.
- 카드 뒷면: 흰 바탕 + accent 2px 테두리(12px) + 안쪽 accent 1px 선(8px) + 가운데 accent-soft 원과 초록 별 + 위아래 작은 점. 22장 모두 같은 뒷면.
- 아이콘: 20px 선 아이콘(선 굵기 1.67) — chevron-left · download · share · refresh · home · lock · copy. 색은 글씨색을 따라감.
- 주제 칩의 이모지(💼💰💕🌿📚✨)는 와이어프레임용이고, **구현할 때 SVG 아이콘으로 바꿉니다** (팩 04).

## 7. 움직임 (Motion) — 카드 고르기 · 뒤집기 (F-3)

| 단계 | 화면 | 움직임 |
|---|---|---|
| 1. 덱 등장 | S-03-P | 22장 뒷면이 **부채꼴(반지름 430px, 카드 사이 8°)**로 펼쳐짐. 가운데부터 아래→위로 0.02초씩 차례로 |
| 2. 넘기기 | S-03-P | 좌우 스와이프 → 덱 전체(wheel 1개)가 회전 (quickTo 0.45초). 손을 떼면 속도를 반영한 뒤 8° 간격에 맞춰 멈춤 |
| 3. 고르기 | S-03-P2 | 탭한 카드가 가운데로 0.5초 (scale 1.7, 180 × 300) + picked 그림자 |
| 4. 뒤집기 | S-03-D | rotateY 180° 0.6초 (90°에서 앞면으로 바뀜). 앞면은 **22장 중 무작위 · 정방향** (고른 뒷면과 무관) |
| 5. 결과로 | S-03 | 0.4초 뒤 카드가 결과 카드 자리로 이동(FLIP 0.5초) → 해석 줄이 0.08초씩 차례로 |

- `transform` · `opacity`만 움직입니다.
- `prefers-reduced-motion: reduce`이면 모든 시간을 **4배 빠르게**(¼).
- 고르기 ~ 결과 이동 중에는 다른 카드 탭 · 뒤로 가기를 막아 두 번 뽑히지 않게 합니다.
- 토스트: 아래에서 올라오며 나타남 200ms, 2.5초 뒤 사라짐.

## 8. 컴포넌트 (디자인 팩 + shadcn/ui)

shadcn 규칙: 색은 의미 토큰(`bg-primary`, `text-muted-foreground`)으로만, `className`은 배치에만, 아이콘은 `data-icon`, 세로 쌓기는 `gap-*`.

### 8-1. 화면 ↔ 컴포넌트 지도

| 화면 | 요소 | 팩 컴포넌트 | shadcn / 구현 | 기능 |
|---|---|---|---|---|
| S-01 시작 | 타이틀 · 소개 | — | `type-display`, `type-body` | F-1 |
| | 카드 3장 부채꼴 (XVII 별 · XVIII 달 · XIX 태양) | Tarot Card / Front (128 × 214) | 커스텀 `TarotCard` | F-1 |
| | [타로 시작] | Button Primary L | `Button size="lg"` | F-1 |
| | ※ 오락용 · 저장 안 해요 | — | `p.type-caption text-muted-foreground` | 원칙 1 · 4 |
| S-02 내 정보 | 앱바 "나에 대해 알려 주세요" | App Bar | `header` + `Button variant="ghost" size="icon"` | F-2 |
| | 이름 · 생년월일 · 전공 | Input | `FieldGroup` > `Field` + `Input` | F-2 |
| | 주제 6개 | Topic Chip | `FieldSet` + `ToggleGroup` (단일) | F-2 |
| | 개인정보 안내 | Privacy Notice | `Alert` (variant `notice`) | 원칙 1 |
| | [카드 한 장 뽑기] | Button Primary/Disabled L | `Button size="lg"` + `disabled` | F-2 · F-3 |
| **S-03-P 카드 고르기** | "{주제}를 떠올리며 카드 한 장을 골라 주세요" | — | `type-title` | F-3 |
| | 22장 부채꼴 덱 | Tarot Card / Back (108 × 180) | 커스텀 `CardDeck` (`role="listbox"`) | F-3 |
| | Swipe! 안내 | — | accent-illust 화살표 + `type-headline` + `type-caption` | F-3 |
| **S-03-P2 선택됨** | 가운데로 올라온 카드 | Tarot Card / Back (180 × 300) + picked 그림자 | `CardDeck` 상태 | F-3 |
| **S-03-D 카드 공개** | "XIX 태양이 나왔어요" + 앞면 (208 × 348) | Tarot Card / 19 The Sun | `TarotCard` + `aria-live="polite"` | F-3 |
| S-03 결과 | 결과 카드 | Result Card | `Card` (Header · Content · Footer) | F-4 |
| | [이미지 저장] · [결과 공유] | Button Secondary M · **Primary M** | `Button variant="secondary"` · `Button` | F-5 · F-6 |
| | [다시 뽑기] · [처음으로] | Button Secondary M ×2 | `Button variant="secondary"` | F-7 |
| | 개인정보 안내 | Privacy Notice | `Alert` notice | 원칙 1 |
| | 저장 · 복사 알림 | Toast | `toast` (Base UI) / `sonner` (Radix) | F-5 · F-6 |
| | 길게 눌러 저장 · 복사 | — | `Drawer` + `DrawerTitle` | F-5 · F-6 |

### 8-2. 앱바 (App Bar)

| 속성 | 값 |
|---|---|
| 크기 | 375 × 56, 좌우 16px, 요소 간격 8px |
| 왼쪽 | chevron-left 20px (누르는 영역 44 × 44), `aria-label="뒤로"` — S-01에는 없음 |
| 가운데 | 제목 Headline 18 Bold, text/primary, 가운데 정렬 |
| 오른쪽 | 20px 빈 자리(제목을 가운데에 두기 위해) |
| 바탕 | 투명 (화면 bg가 보임) |
| 제목 | S-02 "나에 대해 알려 주세요" · S-03-P/P2/D "카드 뽑기" · S-03 "오늘의 타로" |

### 8-3. 버튼 (Button)

| Type | 바탕 | 글씨 | 테두리 | 쓰는 곳 |
|---|---|---|---|---|
| Primary | accent `#00D959` | text/on-accent `#000000` | 없음 | [타로 시작], [카드 한 장 뽑기], [결과 공유] — **화면당 1개** |
| Secondary | surface `#FFFFFF` | text/primary | 1px border | [이미지 저장], [다시 뽑기], [처음으로], Drawer [닫기] |
| Disabled | disabled `#D7D7D7` | 흰색 | 없음 | 이름 · 생년월일 · 주제 중 하나라도 비었을 때 [카드 한 장 뽑기] |

| Size | 크기 | 모서리 | 글씨 | 쓰는 곳 |
|---|---|---|---|---|
| L | 335 × 56 | 16px | Body Bold 16/24 | 화면 하단 주요 행동 |
| M | 162 × 48 | 14px | Label 15/22 | 결과 화면 2 × 2 |

| 상태 | 규칙 |
|---|---|
| hover · active | Primary: 바탕을 5% 어둡게 (`brightness-95`). Secondary: 바탕 surface-sub |
| focus-visible | 2px accent 링, 2px 띄움 (`ring-2 ring-ring ring-offset-2 ring-offset-background`) |
| disabled | 위 Disabled 모양, `disabled` 속성, `pointer-events-none` |
| 처리 중 | `<Spinner data-icon="inline-start" />` + `disabled` (이미지 만드는 중) |

- 아이콘 20px, 라벨과 간격 6px. `<DownloadIcon data-icon="inline-start" />이미지 저장`. 아이콘에 크기 클래스를 붙이지 않습니다.
- 결과 화면 버튼 아이콘: 이미지 저장 = download · 결과 공유 = share · 다시 뽑기 = refresh · 처음으로 = home.

```tsx
<Button size="lg" className="w-full" disabled={!canDraw}>카드 한 장 뽑기</Button>

<div className="grid grid-cols-2 gap-[11px]">
  <Button variant="secondary"><DownloadIcon data-icon="inline-start" />이미지 저장</Button>
  <Button><Share2Icon data-icon="inline-start" />결과 공유</Button>
  <Button variant="secondary"><RotateCwIcon data-icon="inline-start" />다시 뽑기</Button>
  <Button variant="secondary"><HomeIcon data-icon="inline-start" />처음으로</Button>
</div>
```

### 8-4. 입력 (Input) — S-02

| 부분 | 값 |
|---|---|
| 라벨 | Caption Bold 13/19, text/secondary |
| 입력칸 | 335 × 52, surface, 1px border, 모서리 12px, 좌우 16px |
| 값 | Body 16/26 text/primary · 플레이스홀더 text/tertiary |
| 도움말 · 오류 | Caption 13/19 (오류일 때 danger) |
| 간격 | 라벨 ↔ 입력칸 ↔ 도움말 8px |

| State | 테두리 | 그 밖 |
|---|---|---|
| Default | 1px border | 플레이스홀더 |
| Filled | 1px border | 값 text/primary |
| Focused | **2px accent** | — |
| Error | **1.5px danger** | "날짜를 다시 확인해 주세요" (danger) · `Field data-invalid` + `Input aria-invalid` |

```tsx
<FieldGroup>
  <Field>
    <FieldLabel htmlFor="name">이름 (닉네임 OK)</FieldLabel>
    <Input id="name" maxLength={10} autoComplete="off" placeholder="지민" />
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

- 이름 최대 10자, 닉네임 권장(이미지 · 공유 글에 들어감).
- 생년월일: 숫자 8자리 → `YYYY.MM.DD` 자동 점. 없는 날짜 · 미래 날짜는 Error.
- 전공은 6개 계열(인문 · 사회 · 경영 · 자연 · 공학 · 예체능)로 맞추고, 못 맞추면 해석 3줄째를 뺍니다.
- 모든 입력 `autoComplete="off"`, 브라우저 저장소에 쓰지 않음.

### 8-5. 주제 칩 (Topic Chip → ToggleGroup)

| State | 바탕 | 글씨 | 테두리 |
|---|---|---|---|
| Default | surface | Label 15 Medium, text/secondary | 1px border |
| Selected (`data-state="on"`) | accent-soft | **Label 15 Bold, accent-strong** | **1.5px accent** |
| focus-visible | — | — | 2px accent 링 |

- 105 × 44, 모서리 22px, 3열 × 2줄, 가로 · 세로 간격 10px.
- 순서 고정: 커리어 · 재물 · 연애 · 건강 · 학업 · 종합. 6개 중 하나만.
- 질문 "어떤 주제가 궁금한가요?"는 Title 22 Bold (`FieldLegend`).

### 8-6. 개인정보 안내 (Privacy Notice → Alert notice)

- 335 폭, surface-sub 바탕, 테두리 없음, 모서리 12px, 안쪽 위아래 14 · 좌우 16px, lock 아이콘 20px + 간격 10px, Caption 13/19 text/secondary.
- 문구(고정):
  - S-02: "입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요."
  - S-03: "정보는 저장되지 않아요. [처음으로]를 누르면 바로 지워져요."

### 8-7. 토스트 (Toast)

- inverse `#232427` 바탕, 흰 글씨 Label 15, 모서리 12px, 안쪽 14 / 20px, **앱바 아래 8px 가운데**. 결과 화면 아래쪽은 버튼 · 개인정보 안내로 차 있어서, 토스트가 안내를 가리지 않게 위에 띄웁니다.
- 문구: "이미지를 저장했어요" · "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요".

### 8-8. 타로 카드 (Tarot Card)

| 종류 | 크기 | 모양 |
|---|---|---|
| Back (덱) | 108 × 180 | 흰 바탕, accent 1.8px 테두리, 모서리 10.8px (기본 120 × 200 의 0.9배) |
| Back (고른 카드) | 180 × 300 | accent 3px 테두리, 모서리 18px, picked 그림자 |
| Front (결과 카드 안) | 160 × 268 | 그림 꽉 채움(FILL), 모서리 10px, card 그림자 |
| Front (공개 화면) | 208 × 348 | 같은 모양 1.3배 |
| Front (시작 화면 부채꼴) | 128 × 214 | 같은 모양 0.8배, 3장 겹쳐 펼침 |

- 접근성: `role="img"` + `aria-label="XIX 태양 카드"`. 덱은 `role="listbox"`, 각 카드 `role="option"` + 좌우 화살표 키로 넘기고 Enter로 고름.
- 정방향만(역방향 없음 — MVP 범위).

### 8-9. 결과 카드 (Result Card → Card) — 저장 이미지 영역

| 칸 | 내용 | 스타일 |
|---|---|---|
| `CardHeader` | "지민님의 타로 · 커리어" | Caption Bold 13, text/secondary, 가운데 |
| `CardContent` 1 | 카드 앞면 160 × 268 | card 그림자 |
| `CardContent` 2 | "XIX 태양 · 사자자리" | Headline 18 Bold, **accent-strong** |
| `CardContent` 3 | 해석 3줄 (줄 사이 2px) | Body 16/26, text/primary, 가운데 |
| `CardFooter` | "※ 오락용 타로 해석입니다" | Caption 13, text/tertiary |

- 335 폭, surface, 모서리 24px, 안쪽 위아래 28 · 좌우 24px, 요소 간격 16px, 그림자 없음.
- 해석: 줄1 = 카드 × 주제 기본 문장(이름 포함), 줄2 = 별자리 문장, 줄3 = 전공 계열 문장. 전공이 없으면 `Show Major Line` 끄기(3줄째 없음).
- 건강 · 재물은 단정하지 않고 돌아볼 관점으로 씁니다.
- 생년월일 · 전공 원문은 넣지 않습니다(원칙 2).

### 8-10. 대체 화면 (Drawer) — F-5 · F-6

| 상황 | 처리 |
|---|---|
| 이미지 저장 성공 | 토스트 "이미지를 저장했어요" |
| 이미지 저장 안 됨 (인앱 브라우저) | Drawer "이미지를 길게 눌러 저장해 주세요" + 결과 이미지 미리보기 |
| 공유 메뉴 열림 / 취소 | 결과 화면 그대로 |
| 공유 메뉴 없음 → 자동 복사 성공 | 토스트 "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요" |
| 복사도 실패 | Drawer "아래 글을 길게 눌러 복사해 주세요" + 공유 글 (surface-sub 상자) |

- Drawer: surface 바탕, 위쪽 모서리 24px, 안쪽 24px, 손잡이 40 × 4(border 색), `DrawerTitle` 필수(Headline 18), 아래 [닫기] Secondary L. 뒤 배경은 검정 40%.
- Drawer 안 이미지 · 글은 `user-select: text`, `-webkit-touch-callout: default`.

## 9. 저장 이미지 (1080 × 1350, F-5)

결과 카드를 1080 × 1350 세로 이미지로 만듭니다.

| 영역 | 값 |
|---|---|
| 바탕 | bg `#F3F3F5` 전체, 위아래 48px · 좌우 72px, 요소 간격 28px |
| 결과 카드 | surface, 모서리 72px, 안쪽 위아래 52px · 좌우 72px, 요소 간격 28px |
| 제목 | "지민님의 타로 · 커리어" Bold 40/56 text/secondary |
| 카드 그림 | 336 × 563 (2.1배), card 그림자 |
| 카드 이름 줄 | "XIX 태양 · 사자자리" Bold 54/72 accent-strong |
| 해석 3줄 | Regular 44 / 줄 높이 64, text/primary, 가운데 |
| 오락용 안내 | Regular 34/48 text/tertiary |
| 맨 아래 | 카드 밖 "오늘의 타로" Bold 34/48 text/primary |
| 넣지 않는 것 | 생년월일, 전공 원문, 버튼, 개인정보 안내 |

## 10. 공유 메시지 (F-6)

```
🔮 {이름}님의 타로 · {주제}
{카드 이름} · {별자리}
{해석 3줄}
※ 오락용 타로 해석입니다
나도 한 장 뽑기 → {시작 링크}
```

- 생년월일 · 전공 원문 없음(원칙 2). 링크는 시작 화면, 이름 · 결과 미포함(원칙 5).

## 11. 문구 톤

- 해요체로, 짧게. "~할 때예요", "~돌아볼 때예요".
- 건강 · 재물은 단정하지 않습니다. ✕ "돈을 벌게 됩니다" → ○ "지출 우선순위를 돌아볼 때예요".
- 해석 첫 줄은 "{이름}님,"으로 시작합니다.
- 카드 고르기 안내: "{주제}를 떠올리며 카드 한 장을 골라 주세요" → "선택한 카드를 뒤집어 볼게요" → "{카드 이름}이 나왔어요".

## 12. Do's and Don'ts

### Do

- 화면 바탕은 bg `#F3F3F5`, 카드 · 입력칸은 surface `#FFFFFF`.
- Primary 버튼은 accent `#00D959` 바탕 + **검정 글씨**, 화면당 하나.
- 연두 계열 글씨는 accent-strong `#007A37`로.
- 카드 그림은 RWS 1909 그림을 꽉 채우고, 한글 이름은 카드 밖에 따로.
- 버튼 L 16px · M 14px, 입력 12px, 결과 카드 24px 모서리.
- 해석 본문은 Body 16/26 가운데 정렬, 3줄 · 90자 이내.
- 모든 터치 영역 44px 이상, 입력 글씨 16px.

### Don't

- 흰 글씨를 `#00D959` 위에 쓰지 않습니다(1.9:1).
- `#00D959` · `#00DE00`을 본문 글씨 색으로 쓰지 않습니다.
- 카드 그림 외 요소(버튼 · 결과 카드 · 입력칸)에 그림자를 넣지 않습니다.
- 한 화면에 Primary 버튼을 두 개 두지 않습니다.
- 결과 카드 · 저장 이미지 · 공유 글에 생년월일이나 전공 원문을 넣지 않습니다.
- 다크 모드용 값(v1 Midnight · Candle Gold)을 섞어 쓰지 않습니다.
- `space-y-*`, 직접 쓴 `dark:` 색, `bg-[#...]` 같은 날 값 색을 컴포넌트에 쓰지 않습니다.

## 13. Tailwind v4 · shadcn 테마 (globals.css)

shadcn의 `tailwindCssFile`에만 넣습니다. hex 값은 그대로 씁니다.

```css
@import "tailwindcss";
@import "tw-animate-css";

:root {
  /* shadcn 의미 토큰 → 디자인 팩 */
  --background: #f3f3f5;            /* bg */
  --foreground: #000000;            /* text/primary */
  --card: #ffffff;                  /* surface */
  --card-foreground: #000000;
  --popover: #ffffff;
  --popover-foreground: #000000;
  --primary: #00d959;               /* accent */
  --primary-foreground: #000000;    /* text/on-accent (팩 #fff → 대비 때문에 검정) */
  --secondary: #ffffff;             /* Secondary 버튼 = surface + border */
  --secondary-foreground: #000000;
  --muted: #f6f6f8;                 /* surface-sub */
  --muted-foreground: #676e6a;      /* text/tertiary (팩 #979f9b → 진하게) */
  --accent: #e6faef;                /* accent-soft: 선택된 칩 */
  --accent-foreground: #007a37;     /* accent-strong */
  --destructive: #c9353b;           /* danger (팩 #e5484d → 진하게) */
  --border: #dcdcdd;
  --input: #dcdcdd;
  --ring: #00d959;

  /* 이름 있는 토큰 */
  --text-secondary: #4d4d4e;
  --accent-strong: #007a37;
  --accent-illust: #00de00;
  --disabled: #d7d7d7;
  --inverse: #232427;
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
  --color-text-secondary: var(--text-secondary);
  --color-accent-strong: var(--accent-strong);
  --color-accent-illust: var(--accent-illust);
  --color-disabled: var(--disabled);
  --color-inverse: var(--inverse);

  --font-sans: "Noto Sans KR", system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;

  /* 둥근 모서리 — 컴포넌트가 쓰는 클래스에 고정 */
  --radius-sm: 8px;      /* 카드 뒷면 안쪽 선 */
  --radius-md: 10px;     /* 타로 카드 앞면 */
  --radius-lg: 12px;     /* 입력칸, Notice, 토스트 */
  --radius-xl: 14px;     /* M 버튼 */
  --radius-2xl: 16px;    /* L 버튼 */
  --radius-3xl: 24px;    /* 결과 카드, Drawer */
  --radius-4xl: 9999px;  /* 칩 */
}

@theme {
  --shadow-xs: 0 0 #0000;
  --shadow-sm: 0 0 #0000;
  --shadow-card: 0 6px 16px rgba(0, 0, 0, 0.12);
  --shadow-picked: 0 10px 28px rgba(0, 217, 89, 0.35);

  --animate-flip: flip 600ms cubic-bezier(0.2, 0.7, 0.2, 1) both;
  --animate-rise: rise 250ms ease-out both;

  @keyframes flip {
    from { transform: rotateY(0deg); }
    to { transform: rotateY(180deg); }
  }
  @keyframes rise {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }
}

/* 글씨 스타일 — 모두 자간 -2% */
@utility type-display { font-size: 28px; line-height: 38px; font-weight: 700; letter-spacing: -0.02em; }
@utility type-title { font-size: 22px; line-height: 32px; font-weight: 700; letter-spacing: -0.02em; }
@utility type-headline { font-size: 18px; line-height: 26px; font-weight: 700; letter-spacing: -0.02em; }
@utility type-body { font-size: 16px; line-height: 26px; font-weight: 400; letter-spacing: -0.02em; }
@utility type-body-bold { font-size: 16px; line-height: 24px; font-weight: 700; letter-spacing: -0.02em; }
@utility type-label { font-size: 15px; line-height: 22px; font-weight: 500; letter-spacing: -0.02em; }
@utility type-caption { font-size: 13px; line-height: 19px; font-weight: 400; letter-spacing: -0.02em; }
@utility type-caption-bold { font-size: 13px; line-height: 19px; font-weight: 700; letter-spacing: -0.02em; }

@layer base {
  * { @apply border-border outline-ring/50; }
  html { color-scheme: light; }
  body {
    @apply bg-background text-foreground font-sans antialiased;
    word-break: keep-all;
  }
  input { font-size: 16px; }
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
      animation-duration: calc(var(--tw-duration, 1s) / 4) !important;
      transition-duration: calc(var(--tw-duration, 1s) / 4) !important;
    }
  }
}
```

### shadcn 시작 방법

- 스타일: **`maia`** — 40px 이상 컨트롤, 12px 이상 모서리, 여유 있는 간격이 디자인 팩과 가장 가깝습니다.
- 처음 만들 때: `npx shadcn@latest init --base base --preset maia --template vite --name taro --no-monorepo -y`
- 필요한 컴포넌트: `npx shadcn@latest add button card field input toggle-group alert toast drawer spinner`
- `button.tsx`의 `cva` size: `lg` = h-14(56) · rounded-2xl, `default` = h-12(48) · rounded-xl. `input.tsx` = h-13(52) · rounded-lg.
- `Alert`에 `notice` variant를 더합니다(muted 바탕, 테두리 없음, `text-secondary`).
- 덱(`CardDeck`)과 카드(`TarotCard`)는 shadcn에 없어 직접 만듭니다. 스와이프 · FLIP 애니메이션은 GSAP(quickTo · Flip) 기준으로 적혀 있습니다(팩 05).

## 14. 미정 (Known Gaps)

- 주제 칩 SVG 아이콘 6종 (팩: 이모지는 와이어프레임용) — 아이콘 세트 정하기.
- 덱 스와이프 라이브러리: 팩 문구는 GSAP 기준. 다른 라이브러리를 쓰면 시간 값만 유지.
- 카드 그림 원본 출처 표기 위치(서비스 하단 "카드 그림: Rider-Waite-Smith, 1909")를 정할지.
- 라이트 모드만 있음. 다크 모드는 MVP에서 만들지 않음.
- 개인정보 동의 체크가 필요해지면 S-02에 `Field` + `Checkbox` 추가.
