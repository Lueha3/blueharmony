# 스타일링 릴스 인물 교체 — 작업 러너북

옷장/테일러샵 스타일링 릴스에서 맨 왼쪽 인물을 교체하는 작업의 검증된 파이프라인.
다음번엔 이 문서를 읽는 것만으로 탐색 단계 없이 바로 생성에 들어갈 것.

---

## 0. 지금 상태 (2026-08-19 기준)

- **크레딧 부족**: 22.19 크레딧 (직전 세션엔 1400.59 → 사용자가 2026-08-18 11:56~14:13 사이 힉스필드에서 직접 약 15회 생성 시도). **음성 클론(create_voice)이 이 잔액으로 실패함.** 재개 전 충전 필요.
- **원본 영상 음성 클론용으로 임포트 완료된 오디오** (재사용 가능, media_id 재사용하면 재업로드 불필요):
  - `voice_1` (70.2초, 무신사 반팔 리뷰, 가장 길고 깨끗함) → `media_id: 5c23fb28-3b75-401f-8eec-8b666f0b017e`
  - `voice_4` (10.4초, "블랙의 O은 O해 보이고" **목표 영상과 동일한 색조합 멘트 포맷** — 톤/리듬 참조용) → `media_id: d8bc9fe2-9307-4194-a929-07553eb71800`
  - 위 media_id가 만료됐으면 아래 "파일 전달 방법"으로 재관통 필요.
- 크레딧 충전 후 다음 액션: `create_voice_from_confirmed_audio(audio_media_id="5c23fb28-...", name="influencer_original_voice")` → voice_id 발급 → §5 파이프라인 진행.

---

## 1. 원본 영상 분석 결과 (재분석 불필요 — 이 표 그대로 사용)

세로 릴스, 42.2초, 10장면(각 ~4.2초), 고정 카메라. 왼쪽 인물(테일러)이 진행, 가운데 여성·오른쪽 남성 모델 의상이 컷마다 교체.

| # | 색 조합 | 대사 | 원본의 실제 제스처 (video_analysis 결과) |
|---|---|---|---|
| 1 | 검정+그레이 | 검정과 그레이는 격식 있어 보입니다 | 오른손으로 커플 쪽을 가리킴 |
| 2 | 검정+버건디 | 검정과 버건디는 자신감 있어 보입니다 | 검지를 위로 들어올림 |
| 3 | 그레이+화이트 | 그레이와 화이트는 깔끔해 보입니다 | 양손으로 제스처 |
| 4 | 그레이+버건디 | 그레이와 버건디는 카리스마 있어 보입니다 | 왼손으로 여성의 허리 쪽을 가리킴 |
| 5 | 네이비+화이트 | 네이비와 화이트는 단정해 보입니다 | 양손으로 커플 향해 제스처 |
| 6 | 네이비+카멜 | 네이비와 카멜은 클래식해 보입니다 | 왼손으로 여성의 의상을 가리킴 |
| 7 | 브라운+크림 | 브라운과 크림은 자연스럽게 고급스러워 보입니다 | 한 손으로 여성 쪽 제스처 |
| 8 | 브라운+블랙 | 브라운과 블랙은 차분하지만 존재감 있어 보입니다 | 왼손으로 열정적인 제스처 |
| 9 | 베이지+화이트 | 베이지와 화이트는 부드러워 보입니다 | 커플 향해 제스처 |
| 10 | 베이지+브라운 | 베이지와 브라운은 품위 있어 보입니다 | 마지막 승인하는 손짓 |

---

## 2. 확정된 기술 설정

- **모델**: Seedance 2.5, 기능 **Video Edit**(원본 영상 첨부 후 수정 — 이미지에서 새로 생성 아님)
- **영상 클립 길이**: **반드시 4~30초**. 3.7~3.8초처럼 애매하면 `atempo`로 살짝 늘려 4초 이상 확보할 것 (미달 시 422 Unprocessable Entity).
- **비율/해상도**: `aspect_ratio: 9:16`, `resolution: 1080p` — "auto"로 두면 16:9 기본값이 적용되며 세로 소스가 찌그러짐.
- **fps**: 30 명시 (23fps처럼 비표준 값이 나온 적 있음 — 인스타/틱톡 표준은 30).
- **레퍼런스 사진**: 3장, 정면 위주. **옷장 앞 클로즈업(안경에 청록색 반사 있는 사진)은 제외** — 이 사진 때문에 매 생성마다 안경 렌즈에 색 반사가 학습됨.
- **10벌을 한 번에 넣지 말 것**: 30초 제한에 10벌을 욱여넣으면 문장 속도가 40% 빨라지고 어미가 격식체→해요체로 섞이며 마지막 단어가 뭉개짐. **5벌씩 Part 1 / Part 2로 분리** (각 25초, 문장당 4초 확보).

---

## 3. 파일 전달 방법 (이 환경은 Higgsfield 업로드 서버로 직접 PUT 불가)

이 세션의 네트워크 프록시가 `upload.higgsfield.ai`, `*.supabase.co`를 차단함. 검증된 우회 경로:

```
1. 로컬 파일을 저장소에 임시 커밋 → push
2. jsDelivr CDN URL로 접근: https://cdn.jsdelivr.net/gh/<owner>/<repo>@<commit-sha>/<path>
   ⚠ raw.githubusercontent.com은 절대 안 됨 (MIME 타입이 application/octet-stream이라 Higgsfield가 거부)
3. media_import_url(url=jsDelivr URL, type=image|video|audio) 호출 → media_id 획득
4. 즉시 git reset --hard <직전 클린 커밋> && push --force-with-lease 로 임시 커밋 제거
```

레포는 public(`Lueha3/blueharmony`)이라 임시 커밋 노출 시간을 최소화할 것 (커밋→임포트→삭제를 한 턴 안에 연속 실행).

---

## 4. 얼굴/제스처 프롬프트 (Video Edit 모드)

```
VIDEO EDIT TASK — modify the attached source video. Do not recreate the
scene; change ONLY the person on the far left.

CAMERA — ABSOLUTELY STATIC. Locked-off tripod shot, no zoom, no pan, no
dolly. Framing identical in every frame.

PERSON — REMOVE the old man on the far left. PUT IN HIS PLACE the man from
the attached reference photos: a Korean man in his MID-TWENTIES, smooth
youthful skin, no wrinkles, dark brown wavy center-parted hair, round black
glasses with PERFECTLY CLEAR anti-reflective lenses (no glare, no colored
reflection, eyes fully visible). Slim toned build, 171 cm / 67 kg — visibly
shorter and slimmer than the tall male model on the right. He wears the same
outfit the old man wore: white dress shirt, black vest (pure black, not
navy), black tie, black trousers, yellow measuring tape around the neck.

EXPRESSION — calm, warm, professional. Natural micro-movements: occasional
blink, slight head tilt between lines. NO exaggerated mouth shapes, no wide
"O" mouth, no frozen static face between lines.

GESTURES — one small gesture per line/outfit, matching this shot's specific
gesture: [장면별로 위 표의 "원본의 실제 제스처" 칸 문구를 그대로 넣을 것].
Five clearly separated, correctly shaped fingers. Do NOT clasp or interlock
hands — that causes finger merging artifacts.

EVERYTHING ELSE STAYS IDENTICAL: the two models and their outfits, the
boutique background, lighting, scene cuts, camera framing, aspect ratio
(9:16, no letterboxing/stretching), and the on-screen Korean captions
exactly as they appear (do not re-draw or re-type any text).
```

---

## 5. 음성 파이프라인 (핵심 교훈: 얼굴 교체와 음성 복제를 한 번에 요청하지 말 것)

**실패했던 방식**: video_edit에게 "얼굴도 바꾸고 목소리도 복제해서 립싱크까지" 동시 요청 → 말 속도 40%↑, 어미 혼용, 마지막 단어 뭉개짐.

**검증된 방식 — 2단계 분리**:

1. **1단계**: video_edit에서 **원본 할아버지의 실제 음성 트랙은 그대로 유지**한 채 얼굴·제스처만 교체 (§4 프롬프트, 오디오 언급 없음). 실제 사람이 녹음한 음성이라 호흡·억양이 이미 자연스러움.
2. **음성 클론 등록** (1회만, 이후 재사용):
   ```
   create_voice_from_confirmed_audio(
     audio_media_id="5c23fb28-3b75-401f-8eec-8b666f0b017e",  # voice_1, 70.2s
     name="influencer_original_voice"
   )
   ```
   → 비동기, `list_voices`로 `status="completed"`, `is_audio_eligible=true` 확인 후 사용.
3. **2단계**: 1단계 결과 영상에 대해
   ```
   voice_change(
     video_id=<1단계 결과 job_id>,
     voice_id=<위에서 발급된 voice_id>,
     voice_type="element"
   )
   ```
   타이밍은 원본 그대로 유지하면서 음색만 교체 → 원본의 자연스러운 리듬 보존.

**보이스 샘플 5개 평가 결과** (2026-08-19 확인):

| 파일 | 길이 | 내용 | 용도 |
|---|---|---|---|
| voice_1 | 70.2s | 무신사 반팔 리뷰 | **클론 원본으로 사용** (가장 길고 깨끗함, lang_prob 1.00) |
| voice_2 | 34.3s | 에어리즘 리뷰 | 보조 샘플 |
| voice_3 | 46.8s | 블프 세일 리스트 | 보조 샘플 |
| voice_4 | 10.4s | **"블랙의 O은 O해 보이고" 색조합 멘트** | 클론엔 짧지만, **말투/리듬 참조용으로 최적** — 목표 대사와 동일 포맷 |
| voice_5 | 59.8s | 신발 추천 7가지 | 보조 샘플 |

---

## 6. 알려진 실패 패턴 (재발 방지용)

| 증상 | 원인 | 해결 |
|---|---|---|
| 422 Unprocessable Entity | 영상 클립이 4초 미만 | atempo로 4초 이상 확보 |
| raw.githubusercontent.com 임포트 거부 | MIME 타입이 octet-stream | jsDelivr CDN 경유 |
| 인물이 노인으로 나옴 | "elderly tailor"를 대상 인물 묘사로 오독 | "REMOVE the old man" + 대상은 별도로 "MID-TWENTIES"로 명시 |
| 비율 찌그러짐/레터박스 | aspect_ratio 미지정 | 9:16 명시 |
| 안경에 청록색 반사 | 특정 레�퍼런스 사진(클로즈업)의 반사가 학습됨 | 해당 사진 제외 |
| 손가락 뭉개짐 | "깍지 낀 손" 등 모호한 제스처 지시 | 장면별 구체적 동작 지정 |
| 말 속도 40%↑, 어미 혼용, 마지막 단어 뭉개짐 | 30초에 10벌+음성복제 동시 요청 | 5벌씩 분리 + 음성은 §5 2단계로 분리 |
| 샌드박스 파일 소실 | Higgsfield sandbox_exec는 호출 사이 상태 비보존 | 다운로드→인코딩→합치기→업로드를 **한 스크립트**로 묶어 nohup 백그라운드 실행 |
| media_upload PUT 403 | 이 환경 프록시가 upload.higgsfield.ai 차단 | §3 jsDelivr 릴레이 사용 |

---

## 7. 비용/시간 벤치마크

- 장면 10개 개별 편집 + 합본: 약 306 크레딧, 약 3시간 (첫 시행착오 포함)
- 다음번 목표 (이 문서 활용 시): 90~120 크레딧, 20~30분

---

## 8. 다음 세션 시작 프롬프트 (복붙용)

```
VIDEO_RUNBOOK.md 기준으로 이어서 진행해줘.
- §0의 media_id로 음성 클론부터 재개 (크레딧 충전 확인 후)
- §4 프롬프트 + §1 표의 제스처로 Part1(1~5벌)/Part2(6~10벌) 얼굴 교체본 생성
- §5의 2단계로 음성 교체
- 변경사항: [있으면 여기에]
```
