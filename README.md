# 윤문 (yoonmoon)

> 한글 글을 **사람처럼 윤문**하고, **번역투를 교정**하고, **맞춤법을 바로잡고**, **문체를 변환**하고,
> **AI가 썼는지 판별**하는 Claude Code 스킬/플러그인

ChatGPT·Claude·Gemini가 쓴 한국어 글에는 번역투, 피동 남용, 상투적 표현, 불릿·이모지 과다 같은
"AI 티"가 묻어난다. 번역된 글에는 번역체가, 모든 글에는 맞춤법·문체 문제가 따라온다. 이 플러그인은
한글 글다듬기를 목적별로 나눈 다섯 스킬과, 이를 전과정으로 묶는 풀코스 스킬을 제공한다:

| 스킬                   | 한 일         | 정체성 (트리거 경계)                                            |
| ---------------------- | ------------- | --------------------------------------------------------------- |
| **`polish-all`**       | 전과정 풀코스 | 진단→교정→번역투→AI티→문체변환→재진단을 *자동 라우팅*해 한 번에 |
| **`humanize`**         | AI 글 윤문    | *AI가 쓴 글*의 AI 티 제거 (문체 유지)                           |
| **`translate-polish`** | 번역투 교정   | _번역된 글_(번역서·MT·MTPE)의 번역체 교정 (재번역 아님)         |
| **`proofread`**        | 교정·교열     | 맞춤법·띄어쓰기·문법·비문 등 *객관적 오류*만 (뜻·문체 불변)     |
| **`restyle`**          | 문체·톤 변환  | 격식·매체에 맞춰 register _의도적 변경_                         |
| **`detect`**           | AI 작성 판별  | 고치지 않고 *AI 가능성·신뢰도·근거*만 진단                      |

- ✅ **내용 보존** — 윤문·교정·변환 모두 고유명사·수치·인용·날짜·주장은 한 글자도 바꾸지 않는다
- ✅ **목적별 분리** — 윤문(AI/번역) · 교정(규범) · 변환(문체) · 판별을 섞지 않고 또렷이 나눈다
- ✅ **10대 AI 티 분류 + 8대 번역투 유형** — 체계적 탐지·교정, 규정 근거와 함께 내역 제시
- ✅ **학술 근거** — KatFishNet·LREAD·XDAC, 한국 번역학·번역 보편소(Baker·Toury·Toral) 연구로 뒷받침
- ✅ **단문·SNS·댓글까지** — 문어체뿐 아니라 짧은 구어체 글도 별도 신호축(XDAC)으로 판별
- ✅ **가벼운 단일 흐름** — 별도 에이전트 스폰 없이 빠르게. 장르·강도 조절 가능

## 설치

```text
/plugin marketplace add amondnet/yoonmoon
/plugin install yoonmoon@yoonmoon
```

로컬에서 바로 시험하려면 저장소 경로를 마켓플레이스로 추가한다:

```text
/plugin marketplace add /Volumes/Dev/IdeaProjects/yunmun
/plugin install yoonmoon@yoonmoon
```

## 사용법

여섯 스킬 모두 description으로 **자동 트리거**된다. 한글 텍스트와 함께 말하면 된다.

### 전과정 풀코스 (polish-all) — 진단부터 다듬기까지 한 번에

어떤 단계가 필요한지 모를 때 가장 간단한 진입점이다. `detect`로 입력을 진단해 필요한 단계만 자동
라우팅한 뒤 **교정 → 번역투 제거 → AI 티 제거 → 문체 변환** 순으로 누적 적용하고, 마지막에 재진단한다.

```text
이 글 전체적으로 싹 다듬어줘:

(한글 텍스트 …)
```

옵션: `강도: 보수|기본|적극`, `목표 문체: 하십시오체|해요체|…`(지정 시에만 문체 변환 단계 실행).
번역문이면 원문을 같이 주면 더 정확하다. 한 측면만 필요하면 아래 개별 스킬을 직접 쓴다.

**출력**: ① 한 줄 상태(실행 단계·누적 변경률·재진단 전후) ② 최종 결과물 ③ 단계별 요약 표
④ before→after 하이라이트.

### 윤문 (humanize) — 사람처럼 다듬기

```text
이 글 AI 티 좀 없애줘:

인공지능 기술은 우리 사회의 다양한 측면에 매우 혁신적인 변화를
가져오고 있다고 할 수 있다. 또한, 이러한 변화는 …
```

옵션은 자연어로 덧붙인다:

- `장르: 칼럼 | 리포트 | 블로그 | 공식문서` — 생략 시 자동 추정
- `강도: 보수 | 기본 | 적극` — 생략 시 `기본`

후속 명령도 같은 스킬이 처리한다: "특정 카테고리만 다시", "윤문 강도 조정", "장르 바꿔서", "2차 윤문".

**출력**: ① 한 줄 상태 `완료. 변경률 X% / 등급 Y / 자체검증 N/6 통과` ② 윤문본
③ 카테고리별 탐지 before/after 표 ④ 주요 변경 하이라이트 3~5건.

### 탐지 (detect) — AI 작성 여부 진단

```text
이거 AI가 쓴 글이야? 판별해줘:

(한글 텍스트 …)
```

**출력**: ① 한 줄 판정 `AI 가능성: 높음/중간/낮음 / 신뢰도: …` ② 근거 요약
③ 신호 표 ④ 의심 구간 하이라이트.

**단문·댓글·SNS**도 판별한다 — 입력이 짧은 구어체면 반복문자·포맷팅 결핍, 격식·중립 과다 같은
단문 전용 신호축([XDAC](https://aclanthology.org/2025.acl-long.1108/) 근거)을 자동 적용한다(문어체엔 미적용).

> ⚠️ 탐지는 **확률적 추정**이다. 표절·부정행위 등 불이익 판정의 단독 근거로 쓰지 말 것.
> 사람이 써도 번역투·쉼표 습관이 있어 위양성이 날 수 있다.

### 번역 윤문 (translate-polish) — 번역투 다듬기

번역서·자막·논문, 또는 구글번역·DeepL·파파고 등 **기계번역 결과**의 번역체를 자연스럽게 고친다.
"AI가 썼는지"와 무관하게 *번역된 글*이 대상이다.

```text
이 번역문 번역투 좀 다듬어줘 (원문도 같이 줄게):

이 연구는 우리가 그 문제를 이해하는 것을 가능하게 한다. 그것들은
여러 방법들을 통해 분석되어진다.
```

원문(원천 텍스트)을 같이 주면 명시화·간섭을 대조한다. 옵션: `강도: 보수|기본|적극`.
**재번역이 아니다** — 오역 의심은 고치지 않고 표시만 한다.

### 교정·교열 (proofread) — 맞춤법·문법 바로잡기

문체는 그대로 두고 **맞춤법·띄어쓰기·표준어·외래어 표기·문장부호·비문** 등 객관적 오류만 고친다.
각 교정은 규정 근거와 함께 내역으로 보여준다.

```text
맞춤법 좀 봐줘:

오늘 회의가 잘 됬다. 할수있는 일을 일일히 점검했고 메세지도 보냈다.
```

**출력**: ① 교정 건수(분류별) ② 교정본 ③ `원문 → 교정 + 근거` 내역 표 ④ 확인 요망 항목.
규범으로 분류되지 않는 어색함은 손대지 않는다(그건 윤문 영역).

### 문체·톤 변환 (restyle) — 격식·매체 맞춤

내용은 그대로 두고 **문체·격식·톤만** 목표에 맞게 바꾼다. humanize가 문체를 *유지*한다면 restyle은
문체를 _의도적으로 바꾼다_.

```text
이 글 비즈니스 이메일 톤(하십시오체)으로 바꿔줘:

야 그거 언제까지 줄 수 있어? 빨리 좀 해줘.
```

종결체(하십시오체/해요체/한다체/반말)·매체(보도자료·이메일·CS·마케팅·SNS·학술 등)를 지정한다.
종결 통일·높임 정합·어휘 격식·호칭까지 함께 조정한다.

## 프로젝트별 단어 사전·규칙 (.yoonmoon.md)

프로젝트 루트에 `.yoonmoon.md` 파일을 두면, 모든 스킬이 작업 시작 시 자동으로 읽어 **프로젝트별 단어
사전과 규칙**을 반영한다. 브랜드명 보존, 조직 표준 표기 강제, 금칙어, 기본 옵션(장르·강도·종결체),
카테고리 예외 등을 한 파일로 지정할 수 있다.

```markdown
# .yoonmoon.md

## 보존 사전        # 절대 바꾸지 않을 표현 (브랜드·제품명·고유 용어)
- 다이어트친구
- DietFriends

## 치환 사전        # 강제 치환 (A → B)
유저 → 사용자
어플 → 앱

## 금칙어           # 우선 제거 대상
- ~에 대해
- ~을 통해

## 기본 옵션        # 대화에서 직접 지정한 옵션이 항상 우선
genre: 공식문서
intensity: 기본
register: 해요체

## 예외 규칙        # 자유 산문 규칙
- 카테고리 10(영어 인용)은 검사하지 않는다 — 기술 용어 원어 병기 허용.
```

- **탐색**: 현재 디렉터리에서 상위로 올라가며 가장 가까운 `.yoonmoon.md`를 찾는다(git 동작과 유사).
  파일이 없으면 스킬 기본값으로 동작한다(기능은 전적으로 선택).
- **우선순위**: 대화에서 직접 지정한 옵션 > `.yoonmoon.md` > 스킬 기본값. 사전 간에는 **보존 사전이 최우선**.
- **스킬별**: humanize·translate-polish·restyle은 사전을 적용해 고쳐 쓰고, proofread는 보존·표준 표기에,
  detect는 위양성 억제·장르 기본값에만 쓴다(글을 고치지 않음).

복사용 템플릿은 [`.yoonmoon.example.md`](.yoonmoon.example.md), 전체 규약은
[`skills/humanize/references/project-config.md`](skills/humanize/references/project-config.md) 참고.

## 10대 AI 티 카테고리

| #   | 카테고리            | 대표 패턴                                          |
| --- | ------------------- | -------------------------------------------------- |
| 1   | 번역투              | "~을 통해", 무생물 주어, 직역 대명사(그/그것/그들) |
| 2   | 피동·사동 남용      | 이중 피동("되어진다"), "~에 의해"                  |
| 3   | 상투적 표현·hedging | "결론적으로", "주목할 만하다", 과장어              |
| 4   | 접속사·연결어 남발  | 문두 "또한/따라서", 연결어미 뒤 쉼표               |
| 5   | 기계적 구조·병렬    | 첫째/둘째/셋째, 불릿 과다, 균일 문장               |
| 6   | 형식명사·명사화     | "것이다", "~하는 것", 한자어 명사화                |
| 7   | 과잉 수식           | "매우" 남발, "-적" 연쇄, 동의어 중첩               |
| 8   | 시각 장식           | 과도한 볼드, 이모지, em-dash(—)                    |
| 9   | 리듬 균일성         | 종결어미·문장 길이·문두 단조                       |
| 10  | 영어 인용 과다      | 불필요한 영어 병기                                 |

자세한 정의·예시·심각도는 [`skills/humanize/references/ai-tell-taxonomy.md`](skills/humanize/references/ai-tell-taxonomy.md) 참고.

## 구조

```text
yoonmoon/
├── .yoonmoon.example.md     # 프로젝트별 설정 템플릿 (.yoonmoon.md로 복사해 사용)
├── .claude-plugin/
│   ├── plugin.json          # 플러그인 매니페스트
│   └── marketplace.json     # 마켓플레이스 등록
├── skills/
│   ├── polish-all/          # 전과정 풀코스 오케스트레이터
│   │   ├── SKILL.md         # 진단·라우팅 → 교정→번역투→AI티→문체변환 → 재진단
│   │   └── references/
│   │       └── pipeline-guide.md  # 단계 순서·라우팅 매트릭스·중복 처리·통합 검증
│   ├── humanize/            # AI 글 윤문(고쳐쓰기) 스킬
│   │   ├── SKILL.md         # 오케스트레이터 (탐지·윤문·검증)
│   │   └── references/
│   │       ├── ai-tell-taxonomy.md    # 10대 AI 티 분류 (humanize·detect 공유)
│   │       ├── project-config.md      # .yoonmoon.md 프로젝트 설정 규약 (전 스킬 공유)
│   │       ├── rewriting-guide.md     # 윤문 원칙·순서·자체검증
│   │       ├── examples.md            # 장르별 before/after
│   │       └── katfishnet-research.md # 근거: 쉼표·POS 다양성 (KatFishNet, ACL 2025)
│   ├── translate-polish/    # 번역투 교정(번역 윤문) 스킬
│   │   ├── SKILL.md         # 번역투 탐지·교정·검증
│   │   └── references/
│   │       ├── translationese-taxonomy.md  # 8대 번역투 유형 분류
│   │       ├── polish-guide.md             # 교정 원칙·순서·원문 활용
│   │       └── translationese-research.md  # 근거: 번역 보편소·post-editese (humanize 공유)
│   ├── proofread/           # 교정·교열(맞춤법·문법) 스킬
│   │   ├── SKILL.md         # 규범 오류 탐지·교정·검증
│   │   └── references/
│   │       └── proofreading-rules.md  # 맞춤법·띄어쓰기·표준어·외래어·부호·비문 규정
│   ├── restyle/             # 문체·톤 변환 스킬
│   │   ├── SKILL.md         # 현재 문체 파악·변환·검증
│   │   └── references/
│   │       └── register-guide.md      # 상대높임 체계·문어/구어·매체별 톤
│   └── detect/              # 탐지(AI 작성 여부 진단) 스킬
│       ├── SKILL.md         # 신호 스캔 → AI 가능성·신뢰도·근거 (taxonomy 공유)
│       └── references/
│           ├── lread-rubric.md  # 근거: 사람 판별 루브릭·fluency trap (LREAD, 2026)
│           └── xdac-research.md # 근거: 단문/SNS·댓글 탐지 신호 (XDAC, ACL 2025)
└── docs/
    ├── research.md          # 연구·참고 자료 큐레이션 모음 (검증된 출처 + 윤문 매핑)
    └── papers/              # 1차 문헌 로컬 사본 (Git LFS) — LREAD 등
```

## 참고 / 영감

한글 humanize 분야의 선행 프로젝트인 [`epoko77-ai/im-not-ai`](https://github.com/epoko77-ai/im-not-ai)
(humanize-korean, MIT)의 구조와 접근에서 영감을 받았다. 윤문의 AI 티 분류·윤문 룰·문서는
일반 언어학·번역학 상식에 기반해 **독자적으로 새로 작성**했다.

AI 티 탐지·교정 기준은 한국어 LLM 텍스트 탐지 연구 **KatFishNet** (Park et al., ACL 2025,
[논문](https://aclanthology.org/2025.acl-long.1030/) · [코드](https://github.com/Shinwoo-Park/katfishnet))과
한국 번역학·번역 보편소·post-editese 연구로 뒷받침된다. 탐지(detect) 스킬은 더해 사람의
AI 판별 루브릭 **LREAD**([arXiv 2601.19913](https://arxiv.org/abs/2601.19913), 2026)와 단문/SNS·댓글 탐지
연구 **XDAC**([ACL 2025](https://aclanthology.org/2025.acl-long.1108/))로 보강된다. 카테고리별 매핑은
[`katfishnet-research.md`](skills/humanize/references/katfishnet-research.md) ·
[`translationese-research.md`](skills/translate-polish/references/translationese-research.md)에 있고,
탐지·스타일로메트리·규범·선행 도구를 아우르는 **연구·참고 자료 전체 모음**은
[`docs/research.md`](docs/research.md)에 정리했다.

## 작성자

이민수 (Minsu Lee, [@amondnet](https://github.com/amondnet))

## 라이선스

[MIT](LICENSE) © 2026 Minsu Lee
