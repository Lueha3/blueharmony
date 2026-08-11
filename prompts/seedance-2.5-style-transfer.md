# Seedance 2.5 — 레퍼런스 영상 스타일 이식 프롬프트

레퍼런스 영상(`holydrip.club` 스타일링 릴스)의 무드/톤/스타일을 분석하고,
제공된 인물 사진(한국인 남성, 170cm / 65kg)에 이식하기 위한 Seedance 2.5 프롬프트.

---

## 1. 레퍼런스 영상 분석

### 1-1. 기술 스펙

| 항목 | 값 |
|---|---|
| 해상도 | 884 × 1920 (세로 9:16) |
| 프레임레이트 | 30 fps |
| 길이 | 63.0초 |
| 코덱 | HEVC / AAC 44.1kHz 스테레오 |
| 오디오 | 62.3초까지 무음 구간 없음 → 끊김 없는 내레이션 + 비트 |

### 1-2. 두 개의 레이어

영상은 **두 겹**으로 되어 있다. 이걸 구분해야 프롬프트가 산으로 가지 않는다.

**레이어 A — 화면녹화 래퍼 (재현 대상 아님)**
아이폰으로 인스타그램 릴스를 화면녹화한 껍데기.
상태바(9:45, 배터리 100), 다이나믹 아일랜드의 빨간 녹화점, "릴스 / 친구" 탭,
우측 좋아요·댓글(1,315)·공유(6,999) 아이콘, 하단 네비게이션 바,
`holydrip.club` 계정 + "The CEO has been cooking with his looks ✨" 캡션.

→ **이건 AI로 생성하면 안 된다.** 텍스트/아이콘이 깨진다.
   필요하면 편집 툴에서 실제 UI 목업을 얹는 게 정답.

**레이어 B — 실제 릴스 콘텐츠 (재현 대상)**
플러스사이즈 남성을 모델로 한 **챕터형 스타일링 튜토리얼**.
`#1 FABRICS → #2 COLLARS → #3 LAYERING → #4 SHOES → #5 EYEWEAR`

### 1-3. 무드 / 톤 / 스타일

**공간**
- 무한 화이트 사이클로라마(seamless white). 소품·가구·벽 일절 없음
- 코너로 갈수록 아주 옅은 쿨그레이 그라데이션
- 발밑에만 부드러운 컨택트 섀도우 → "떠 있지 않게" 잡아주는 유일한 요소

**조명**
- 하이키(high-key). 정면 대형 소프트박스 + 균일한 필
- 얼굴에 그림자가 거의 없음, 피부 톤 평탄
- 안경 렌즈에 작고 부드러운 캐치라이트
- 커머스 룩북 / 이커머스 상세페이지 촬영 조명 그 자체

**카메라**
- 삼각대 고정, 핸드헬드 흔들림 0
- 아이레벨, 정면 정대(dead-on), 50mm 계열의 왜곡 없는 화각
- 기본은 **전신 풀샷**(머리 위 여백 넉넉)
- 간헐적으로 흉상 클로즈업 / 얼굴 클로즈업 / 하체 디테일 컷(바지+신발)
- 움직임은 아주 느린 푸시인 정도

**편집**
- 비트에 붙는 하드컷. 룩 하나당 **1~2초** 유지
- 시그니처는 **워드로브 텔레포트** — 포즈·프레이밍은 그대로, 옷만 순간 교체되는 매치컷
- 트랜지션 효과(디졸브, 와이프) 없음. 무조건 컷

**그래픽 (이 영상의 진짜 정체성)**
- 대문자 지오메트릭 산세리프. 순백 또는 차콜만 사용
- 챕터 타이틀: 큰 대문자 + 그 위에 작게 자간 벌린 `HACK 4`
- **알약형 흰 배지 + 빨간 ❌ / 초록 ✅**
  `❌ SLIM` `✅ CHUNKY SHOES` `❌ THIN FABRIC` `✅ CREW NECK` `✅ WIDE LAPELS`
- **검정 점선 다이어그램** — 어깨 라인, 얼굴 윤곽 타원, 기장 표시, `longer`, `stronger base`
- **우측 세로 스와치 피커** — `COTTON / DENIM / TWILL / LINEN / CO-ORD` + 커서가 클릭
- 인트로: 흰 라운드 카드 스택 메뉴 (썸네일 + 챕터명 + `#1`~`#5`)

**컬러 그레이딩**
- 밝고 중성적. 낮은 콘트라스트, 화이트 밸런스 정확
- 배경·그래픽은 완전 무채색 → **채도는 오직 옷에만** 존재
- 디지털 선명함. 필름 그레인 없음

**전체 느낌 한 줄**
> 프리미엄 앱 온보딩 화면 같은 패션 튜토리얼. 유머 없이 담백하고,
> 자신감 있게 가르치는 톤. "before → after 글로우업"의 소프트셀.

---

## 2. 모델 적용

### 2-1. 사진 속 인물

- 한국인 남성, 20대 초중반
- 170cm / 65kg → **마르고 균형 잡힌 체형**. 어깨 좁은 편, 군살 없음
- 검은 머리, 투블럭 컷 + 옆으로 넘긴 소프트 앞머리, 윗머리에 살짝 웨이브 볼륨
- **두꺼운 검정 아세테이트 라운드(보스턴) 안경** — 인상의 핵심
- 밝은 피부, 깔끔한 턱선, 오똑한 코, 작고 도톰한 입술
- 표정은 차분한 무표정 ~ 옅은 미소

### 2-2. ⚠️ 콘텐츠 논리를 뒤집어야 하는 이유

원본 모델은 플러스사이즈다. 그래서 챕터 주제가 전부
**"체형을 커버하는 법"** — 얇은 원단, 크루넥, 청키 슈즈로 하체 안정화.

170cm / 65kg 슬림 체형에 그 주제를 그대로 얹으면 논리가 안 맞는다.
챕터를 **"슬림한 체형에 볼륨과 비율을 만드는 법"**으로 뒤집는 게 맞다.

| 원본 챕터 | 이식 챕터 | 논리 |
|---|---|---|
| #1 FABRICS (얇은 원단) | **#1 PROPORTION** | 하이웨이스트 + 상의 짧게 → 다리 길이 확보 |
| #2 COLLARS (작은 카라 ❌) | **#2 VOLUME** | 오버핏 상의로 좁은 어깨 보완 |
| #3 LAYERING | **#3 LAYERING** | 레이어로 상체 두께 만들기 (그대로 유지) |
| #4 SHOES (청키) | **#4 SHOES** | 볼륨 스니커즈 / 굽 있는 부츠로 키 보정 |
| #5 EYEWEAR | **#5 EYEWEAR** | 라운드 안경 유지, 프레임 두께 비교 |

---

## 3. Seedance 2.5 프롬프트

> **길이 제약**: Seedance 2.5는 1회 호출 최대 30초.
> 원본이 63초이므로 **세그먼트로 나눠 생성 후 편집 툴에서 이어붙이는 것**을 권장.
> 아래는 8초 × 5 세그먼트 구성.

### 공통 앵커 블록

모든 세그먼트 프롬프트 앞에 이 블록을 붙인다. 인물 일관성의 핵심.

```
SUBJECT ANCHOR — keep identical in every shot:
A slim young Korean man in his early twenties, matching the reference image exactly:
fair skin with a warm undertone, clean-shaven, a slender oval face with a defined
jawline, a straight nose and small full lips. Black two-block haircut — tapered
short sides, soft side-swept fringe, slight wave and volume on top. He wears thick
round black acetate glasses (Boston-style frames) at all times. Lean athletic build,
170 cm and 65 kg: narrow shoulders, flat stomach, no bulk, long clean limbs.
Calm neutral expression, quiet confidence, no exaggerated smiling.

STYLE ANCHOR — keep identical in every shot:
Seamless infinite white studio cyclorama, absolutely no props, furniture or visible
walls, faint cool-grey falloff in the corners, one soft contact shadow pooling under
his shoes. High-key lighting: a large frontal softbox plus even fill, almost no
shadow on the face, flat even skin, a small soft catchlight in each glasses lens.
Locked-off tripod, eye-level, 50 mm lens, dead-on frontal framing, zero handheld
shake. Bright neutral grade, low contrast, accurate white balance, fully desaturated
background — colour exists only in the clothing. Crisp digital sharpness, no film
grain, no vignette, no lens flare. Vertical 9:16 e-commerce lookbook aesthetic.
```

---

### SEG 1 — INTRO / 메뉴 (8초)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, head-to-toe with generous headroom. He stands centered, feet
shoulder-width apart, arms relaxed at his sides, facing camera dead-on. He wears a
plain white crew-neck T-shirt, washed charcoal wide-leg jeans and beige low-profile
sneakers.

Motion: he holds the pose almost perfectly still — one natural breath, one slow
blink, a barely perceptible weight shift. The camera performs one extremely slow
push-in across the full 8 seconds.

Graphics: flat 2D motion-design overlays composited over the shot, crisp uppercase
geometric sans-serif in pure white and charcoal only. Four white rounded-rectangle
cards slide up from the bottom one after another, evenly stacked, each with a small
square garment thumbnail on its left edge and a large uppercase label:
"PROPORTION", "VOLUME", "LAYERING", "SHOES".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 2 — PROPORTION / 하이웨이스트 비교 (8초)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, identical framing and identical pose throughout.

Beat 1 (0-3s): he wears a long untucked white T-shirt over low-rise straight jeans —
the hem falls past his hips, visually shortening his legs.
Beat 2 (3-8s): hard cut on the beat, a wardrobe teleport — the pose, framing and
lighting stay EXACTLY the same, only the clothes change instantly. Now a cropped
boxy white T-shirt tucked into high-waisted pleated wide-leg trousers, with beige
sneakers.

Motion: minimal. He stays planted, breathing naturally, a single blink per beat.

Graphics: a small white pill-shaped badge with a red cross icon reading "LOW RISE"
appears at his waist in beat 1; on the cut it is replaced by a white pill badge with
a green check reading "HIGH WAIST". A thin black dashed horizontal guide line marks
the waistline in both beats. A small tracked-out label "HACK 1" sits above a large
uppercase title "PROPORTION" in the upper third.

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 3 — VOLUME / 오버핏 (8초)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Medium shot framing him from mid-thigh up, then holding.

Beat 1 (0-4s): a tight slim-fit black knit that clings to his narrow frame and
emphasises how slight his shoulders are.
Beat 2 (4-8s): hard cut, wardrobe teleport with identical pose and framing — an
oversized boxy charcoal sweatshirt with dropped shoulder seams and a wide body,
instantly giving him breadth.

Motion: he lifts his chin very slightly on the cut, then settles. Nothing else moves.

Graphics: thin black dashed lines trace the outline of his shoulders in both beats,
widening visibly on the second. A white pill badge with a red cross reads "SLIM FIT"
in beat 1, replaced by a green-check white pill badge reading "DROPPED SHOULDER".
Small tracked-out "HACK 2" above a large uppercase "VOLUME".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 4 — LAYERING / 스와치 UI (8초)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Full-body wide shot, locked off, identical pose held throughout.

He wears a white T-shirt and high-waisted wide-leg trousers as a base. An open
overshirt layers on top and changes three times in rapid hard cuts on the beat —
first washed indigo denim, then olive cotton twill, then a soft ecru linen — pose,
framing and lighting perfectly unchanged between each swap.

Motion: he keeps his hands loosely in his trouser pockets and stays still; only the
garment swaps create movement.

Graphics: a vertical stack of small square fabric swatch cards floats along the right
edge of the frame, each labelled in tiny uppercase — "DENIM", "TWILL", "LINEN" — and
a small white cursor arrow clicks each one in turn, a green check mark popping onto
the swatch as its garment appears on him. Small tracked-out "HACK 3" above a large
uppercase "LAYERING".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### SEG 5 — SHOES + EYEWEAR (8초)

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

Beat 1 (0-4s): tight detail shot cropped from the knees down — high-waisted
wide-leg trousers breaking over the shoes. Flat thin-soled black loafers first, then
a hard cut to chunky white volume sneakers with a thick midsole, same trousers, same
camera position, same floor shadow.
Beat 2 (4-8s): hard cut to a tight head-and-shoulders close-up, eye-level, dead-on.
He wears the thick round black acetate glasses. Very slow push-in.

Motion: in the close-up he blinks once, then gives a small closed-mouth smile in the
final second.

Graphics: in beat 1, a white pill badge with a red cross reads "THIN SOLE",
replaced on the cut by a green-check badge reading "CHUNKY". In beat 2, a thin black
dashed oval traces the outline of his face, and a green-check white pill badge reads
"ROUND FRAME". Small tracked-out "HACK 4 / 5".

No text distortion, no watermark, no UI chrome, no phone interface.
```

---

### 단일 호출 버전 (15초, 빠른 검증용)

세그먼트 5개가 부담스러우면 이거 하나로 톤부터 확인.

```
[SUBJECT ANCHOR] [STYLE ANCHOR]

A vertical 9:16 fashion styling tutorial reel, 15 seconds, cut on the beat.

Shot 1 (0-4s): full-body wide shot, head to toe with generous headroom. He stands
dead-on, arms relaxed, in a long untucked white T-shirt and low-rise straight jeans.
Perfectly still — one breath, one blink.

Shot 2 (4-8s): hard cut. A wardrobe teleport — identical pose, identical framing,
identical lighting, only the clothes change instantly. Now a cropped boxy white tee
tucked into high-waisted pleated wide-leg trousers with chunky white sneakers.

Shot 3 (8-11s): hard cut to a detail shot from the knees down, the wide trousers
breaking over the thick-soled sneakers, soft contact shadow on the white floor.

Shot 4 (11-15s): hard cut to a tight head-and-shoulders close-up, eye-level,
dead-on, thick round black glasses catching a small soft highlight. Extremely slow
push-in. He blinks once and gives a small closed-mouth smile on the last beat.

Graphics: minimal flat white-and-charcoal motion design — a thin black dashed
horizontal guide at the waistline in shots 1 and 2, and one small white pill-shaped
badge with a green check mark reading "HIGH WAIST" appearing on the cut into shot 2.

No text distortion, no watermark, no UI chrome, no phone interface, no on-screen
paragraphs of text.
```

---

### 클린 플레이트 버전 (그래픽 없음 — 권장)

AI의 텍스트 렌더링은 신뢰도가 낮다. **그래픽 없이 깨끗하게 뽑고 자막·배지·점선은
편집 툴(After Effects / CapCut)에서 얹는 것**이 결과물 품질이 가장 높다.

위 프롬프트에서 `Graphics:` 문단을 통째로 삭제하고 마지막 줄을 아래로 교체:

```
Completely clean frame: no text, no captions, no badges, no logos, no watermark,
no user interface elements of any kind.
```

---

## 4. 호출 파라미터

```json
{
  "model": "seedance_2_5",
  "prompt": "<위 프롬프트>",
  "params": {
    "mode": "omni_reference",
    "aspect_ratio": "9:16",
    "duration": 8,
    "resolution": "720p",
    "generate_audio": false,
    "medias": [
      { "role": "image_references", "value": "<사진1 media_id>" },
      { "role": "image_references", "value": "<사진2 media_id>" },
      { "role": "image_references", "value": "<사진3 media_id>" }
    ]
  }
}
```

**설정 근거**

| 파라미터 | 값 | 이유 |
|---|---|---|
| `mode` | `omni_reference` | 사진의 얼굴 아이덴티티를 물고 가야 함 |
| `aspect_ratio` | `9:16` | 원본 884×1920과 동일한 세로 릴스 |
| `duration` | `8` | 세그먼트 단위. 최대 30초까지 가능 |
| `resolution` | `720p` | Seedance 2.5 최대치 (480p/720p만 지원) |
| `generate_audio` | `false` | 원본은 내레이션+비트 구성. 오디오는 따로 붙이는 게 통제 가능 |
| `medias` | 정면·측면 사진 3장 | 각도가 다양할수록 아이덴티티 안정 |

**주의**
- Seedance 2.5는 **720p가 상한**이다. 원본(884×1920)보다 낮다.
  더 높은 해상도가 필요하면 `seedance_2_0`(std 모드, 최대 4K) 또는
  `minimax_h3`(2K)를 검토하거나, 생성 후 `upscale_video`로 2K/4K 업스케일.
- 워드로브 텔레포트는 한 세그먼트에 **2~3회까지**가 안전하다.
  그 이상 넣으면 얼굴이 흔들린다.
- 프레임당 온스크린 텍스트는 **한 덩어리, 대문자, 2단어 이내**로 유지.

---

## 4-1. 힉스필드 웹에서 직접 실행하기 (복붙용)

### 순서

1. **higgsfield.ai** 로그인 → 영상 생성(Video / Generate) 화면으로 이동
2. **모델을 `Seedance 2.5`로 선택**
   - 모델 목록에 Seedance 2.0 / 2.0 Mini도 같이 보인다. **2.5**를 골라야 함
3. **레퍼런스 이미지 업로드** — 브라우저 UI를 잘라낸 사진 3장을 전부 올린다
   - 역할(role)을 고르는 옵션이 있으면 **`image_references`** 로 지정
   - `start_image`로 잡히면 안 된다. 그러면 사진 배경(복도·강의실)이 첫 프레임에 그대로 박힌다
4. **모드를 `omni_reference`** 로 설정 (레퍼런스를 올리면 보통 자동 전환됨)
5. 아래 설정값 입력 후 프롬프트 붙여넣기

### 설정값

| 항목 | 값 |
|---|---|
| Model | `Seedance 2.5` |
| Mode | `omni_reference` |
| Aspect ratio | `9:16` |
| Duration | `15` |
| Resolution | `720p` (2.5의 상한) |
| Generate audio | **끄기** |

### 프롬프트 (전체 복사)

```
A slim young Korean man in his early twenties, matching the reference photos
exactly: fair skin with a warm undertone, clean-shaven, a slender oval face with a
defined jawline, a straight nose and small full lips. Black two-block haircut —
tapered short sides, a soft side-swept fringe, slight wave and volume on top. He
wears thick round black acetate glasses (Boston-style frames) in every shot. Lean
build, 170 cm and 65 kg: narrow shoulders, flat stomach, no bulk, long clean limbs.
Calm neutral expression, quiet confidence, no exaggerated smiling.

Setting and look, identical in every shot: a seamless infinite white studio
cyclorama, absolutely no props, furniture or visible walls, a faint cool-grey
falloff in the corners, and one soft contact shadow pooling under his shoes.
High-key lighting — a large frontal softbox plus even fill, almost no shadow on the
face, flat even skin, a small soft catchlight in each glasses lens. Locked-off
tripod, eye-level, 50 mm lens, dead-on frontal framing, zero handheld shake. Bright
neutral grade, low contrast, accurate white balance, a fully desaturated background
so colour exists only in the clothing. Crisp digital sharpness, no film grain, no
vignette, no lens flare. Vertical 9:16 e-commerce lookbook aesthetic.

A 15-second fashion styling tutorial reel, cut hard on the beat.

Shot 1 (0-4s): full-body wide shot, head to toe with generous headroom. He stands
dead-on, arms relaxed at his sides, feet shoulder-width apart, in a long untucked
white T-shirt and low-rise straight jeans with beige sneakers. He is almost
perfectly still — one natural breath, one slow blink.

Shot 2 (4-8s): hard cut, a wardrobe teleport — the pose, framing and lighting stay
EXACTLY the same and only the clothes change instantly. Now a cropped boxy white
T-shirt tucked into high-waisted pleated wide-leg trousers with chunky white
sneakers.

Shot 3 (8-11s): hard cut to a detail shot framed from the knees down, the wide
trousers breaking over the thick-soled sneakers, soft contact shadow on the white
floor.

Shot 4 (11-15s): hard cut to a tight head-and-shoulders close-up, eye-level,
dead-on, the thick round black glasses catching a small soft highlight. Extremely
slow push-in. He blinks once and gives a small closed-mouth smile on the final beat.

Completely clean frame: no text, no captions, no badges, no logos, no watermark,
no user interface elements of any kind.
```

### 결과 확인 포인트

이 15초로 판단할 것은 딱 네 가지.

1. **얼굴이 사진과 같은 사람인가** — 특히 4번 샷 클로즈업
2. **배경이 순백 무한대로 깔렸는가** — 사진 속 복도/강의실이 새어나오면 실패
3. **2번 컷에서 포즈가 유지된 채 옷만 바뀌는가** — 워드로브 텔레포트가 이 영상의 핵심
4. **조명이 하이키로 평탄한가** — 얼굴에 그림자가 지면 톤이 달라진다

1번이 흔들리면 → 레퍼런스 사진을 얼굴 위주로 더 타이트하게 크롭해서 재업로드.
2번이 흔들리면 → 사진이 `start_image`로 들어갔을 가능성이 높다. role 확인.
3번이 흔들리면 → 컷을 2개로 줄이고 duration을 10초로.

---

## 5. 확인 필요한 점

1. **가로 스크린샷(옷장 배경 데님 셔츠 남성)의 용도**
   업로드된 영상과는 다른 장면이다. 세로 사진 3장을 모델 레퍼런스로 확정하고
   프롬프트를 짰다. 만약 저 옷장 세팅(화이트 행어에 옷이 걸린 워크인 클로짓)도
   재현 대상이면 `STYLE ANCHOR`의 화이트 사이클로라마를 옷장으로 교체하면 된다.

2. **인스타 UI 재현 여부**
   화면녹화 껍데기까지 원한다면 AI 생성이 아니라 편집 툴에서 실제 UI 목업을
   얹는 방식이 맞다.

3. **오디오**
   원본은 63초 내내 끊기지 않는 내레이션 + 비트. 한국어 내레이션 대본이 필요하면
   챕터 구성에 맞춰 별도로 작성 가능.
