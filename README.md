# 내 연구 도구

## 이 도구는

<!-- 한 줄로: 무엇을 넣으면 무엇이 나오는가. 예) arXiv 번호를 넣으면 발표 준비 노트가 notes/ 에 생긴다 -->

## 쓰는 법

인자는 하나만 준다. arXiv 번호, arXiv URL(버전 붙어도 좋다), PDF 파일 중 하나다.

```bash
./paper 2306.05685                        # arXiv 번호 → notes/2306.05685.md
./paper https://arxiv.org/abs/2306.05685v2 # URL/버전 붙은 번호 → 버전을 뺀 notes/2306.05685.md
./paper ~/Downloads/x.pdf                  # PDF → notes/x.md
```

- 논문 본문을 텍스트로 바꿔 `.cache/` 에 두고, `prompt.md` 를 프롬프트로 `opencode run` 에 붙인다.
- `notes/<이름>.md` 에 네 절(## 요약, ## 핵심 주장, ## 실험 설정, ## 발표 때 받을 만한 질문 5개) 한국어 노트를
  저장하고, 저장한 경로와 줄 수를 한 줄로 출력한다.
- 노트 한 편에 1~5분 걸린다. 실패하면 한국어 한 줄을 출력하고 종료 코드 1 로 끝난다.
  - 모델 응답이 비면 빈 노트를 남기지 않는다 — `opencode run --print-logs` 로 원인을 본다.
  - 글자가 없는 PDF(스캔본)면 노트 대신 "텍스트가 없습니다" 로 끝난다.

## 발표 준비에 가져간 것

<!-- 한두 줄: 노트에서 실제 발표 준비에 가져간 것. 노트(notes/)는 발표 전에 커밋한다 -->

## 노트가 틀린 곳

### notes/2404.05228.md ↔ .cache/2404.05228.txt

**틀린 곳 하나: 핵심 주장 3 — "사용자는 AI 지도를 맹목적으로 수용하거나 거부하지 않고"**

노트는 이를 무제한 명제로 썼으나 원문은 그렇지 않다.

- **원문 절 5.4.1**(`Participants who accepted the guidance`)의 첫 문장:
  "The fair machine guidance group included **a few participants who simply followed** the
  AI-based guidance and stated that they did this because 'it was the AI's decision' or
  because they were unsure of their own decisions."
  → 맹목적으로 수용한 사람이 실제로 있었다. 노트가 근거로 든 **5.4.1절이 오히려 이 예외를
  적시한다.**
- 같은 절의 서술에 따르면 49명 중 사유를 검토한 뒤 수용한 사람은 **21 of 49**,
  의심하면서 수용한 사람은 **13 of 49**였다. 즉 "검토 후 판단"도 다수가 아니라 일부였다.
- 원문 **절 1(기여)** 은 같은 사실을 정확히 다르게 표현한다: "**most** participants did not
  blindly accept the guidance from the system and instead they evaluated the information
  provided before deciding whether to adapt" — "**대부분**", not 전부.

**정정**: "대부분의 사용자는 맹목적으로 수용하거나 거부하지 않고 제시된 정보를 검토한 뒤
판단했다"가 원문과 맞다. 다만 이어지는 "의심하면서 따르는 태도는 fair machine guidance
그룹에서만"은 절 5.4.1의 "The phenomenon of questioning but obeying was unique to the fair
machine guidance group"과 일치하므로 그대로 둔다.

수치 자체는 전부 일치했다(99·459·0.03·37/39/13/10·300·20×5·100·0.47 vs 0.23·p<0.05 등).

### notes/2509.04404.md ↔ .cache/2509.04404.txt

대조 대상: `notes/2509.04404.md` ↔ `.cache/2509.04404.txt` (원문 1,304줄 전체).

**결과: 원문에 없거나 값이 다른 수치는 없다.** 노트에 등장하는 수치 토큰을 전부 원문과
하나씩 대조했고, 노트의 모든 수치가 원문에서 그대로 확인된다.

| 노트의 수치 | 원문 근거(줄/절·표) | 판정 |
| --- | --- | --- |
| 참가자 528명, 모집 575명 | 초록 `N=528` / 절 3.2 `recruited 575 participants` | 일치 |
| 16개 직업(고위 8·저위 8) | 절 3.1 `eight high status ... eight low status` | 일치 |
| 1,526개 시나리오, 후보 3명 선택 | 초록·서문 `1,526 scenarios`, 그림 2 캡션 `selected three candidates` | 일치 |
| trials 2,300 → 1,955 → 1,526 | 절 4.1 `from 2,300 to 1,955 ... 1,526` | 일치 |
| 최대 90% | 초록·기여 1 `up to 90%`, 절 4.1 `90% of the time` | 일치 |
| IAT 사전 실시 시 13% 증가 | 초록 `increase by 13%`, 그림 4 캡션, 절 4.1 `13.0%` | 일치 |
| 이력서 16직업 × 8 = 128개 | 절 3.1, 부록 E.1 `total of 128 work histories` | 일치 |
| 검증 참가자 42명(2명 제외), 직업당 4개 선별 | 부록 E.2 `42 participants ... two ... excluded`, 절 3.1 `four most similar validation scores` | 일치 |
| 검증 이력서 64개 → 16,384 문서 | 부록 F.1 `64 work histories ... 16,384 documents` | 일치 |
| 직무기술서 16직업 × 8 = 128개 | 부록 F.1 `128 job descriptions across 16 occupations` | 일치 |
| 6수준 요인(None·Neutral + 4) | 절 3 `six combinations of bias magnitude and direction` | 일치 |
| Cohen's d 0.2 / 0.5 / 0.8 구분 | 절 3.4 `0.2≤d<0.5 ... 0.5≤d<0.8 ... d≥0.8` | 일치 |
| 참가자 528 · 직업 16 · AIC 1812.58 | 부록 N, 표 7 (`1812.58`, 그룹 528/16) | 일치 |
| χ²(1)=7.588, p=.006 | 절 4.1 (Job Status × Task Order) | 일치 |
| 3개 MTE, top 10% 선정률 | 절 3.1·부록 F (E5-mistral-7b-instruct, GritLM-7B, SFR-Embedding-Mistral) | 일치 |
| 인용 표·그림·절 (표 2·3·9, 그림 1·4·5, 절 3.1·3.4·4.1·4.2·5.2·5.4) | 각 캡션·절 표기 존재 | 일치 |

### 부수적 지적 사항 (수치 오류 아님)

- **42명 vs 40명**: 노트의 `검증 참가자 42명(2명 제외)`는 부록 E.2 기준으로 정확하다
  (42 − 2 = 40). 다만 원문 본문 절 3.1은 검증 참여 인원을 `40 participants`로 쓴다 — 같은
  사실의 두 표현으로 갈등은 없다.
- **제외 단위가 겹쳐 쓰임**: 노트 실험 설정의 `주의력 점검·1차 파형 오류 제외 후 528명의
  1,526개`는 575명 → 528명(참가자 단위 제외)과 2,300 → 1,955 → 1,526(시나리오 단위 제외)를
  한 문장으로 압축한 것이다. 두 흐름은 원문에서 별개로 기술된다(절 3.2, 절 4.1).
- **오탈자**: `1차 파형 오류`는 원문 `first wave`의 오역이다(파형 ≠ wave).

## 데이터 규칙

- 이 저장소에는 **공개 데이터와 합성 데이터만** 넣는다.
- 실제(미공개·IRB) 데이터는 넣지 않는다. 로컬에서 꼭 둬야 하면 `data/private/` 에 둔다 — `.gitignore` 로 무시된다.
