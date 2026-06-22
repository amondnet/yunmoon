# 윤문 (yunmoon)

> 한글 AI 글을 **사람처럼 윤문**하고, **AI가 썼는지 판별**하는 Claude Code 스킬/플러그인

ChatGPT·Claude·Gemini가 쓴 한국어 글에는 번역투, 피동 남용, 상투적 표현, 불릿·이모지 과다 같은
"AI 티"가 묻어난다. 이 플러그인은 두 가지 스킬을 묶는다:

- **`yunmoon`** (윤문) — 글의 **내용은 그대로 둔 채** 문체·리듬·표현만 자연스럽게 고쳐 사람이 쓴 듯한 한국어로 만든다.
- **`detect`** (탐지) — 글을 고치지 않고, **AI가 썼는지**를 신호 기반으로 진단해 'AI 가능성·신뢰도·근거'를 보고한다.

- ✅ **내용 보존** — 윤문 시 고유명사·수치·인용·날짜·주장은 한 글자도 바꾸지 않는다
- ✅ **10대 AI 티 분류** — 번역투부터 리듬 균일성까지 체계적으로 탐지·교정
- ✅ **학술 근거** — KatFishNet·LREAD·XDAC 등 한국어 AI 텍스트 탐지 연구(ACL 2025·2026)로 뒷받침
- ✅ **단문·SNS·댓글까지** — 문어체뿐 아니라 짧은 구어체 글도 별도 신호축(XDAC)으로 판별
- ✅ **가벼운 단일 흐름** — 별도 에이전트 스폰 없이 빠르게. 장르·강도 조절 가능

## 설치

```text
/plugin marketplace add amondnet/yunmoon
/plugin install yunmoon@yunmoon
```

로컬에서 바로 시험하려면 저장소 경로를 마켓플레이스로 추가한다:

```text
/plugin marketplace add /Volumes/Dev/IdeaProjects/yunmun
/plugin install yunmoon@yunmoon
```

## 사용법

두 스킬 모두 description으로 **자동 트리거**된다. 한글 텍스트와 함께 말하면 된다.

### 윤문 (yunmoon) — 사람처럼 다듬기

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

자세한 정의·예시·심각도는 [`skills/yunmoon/references/ai-tell-taxonomy.md`](skills/yunmoon/references/ai-tell-taxonomy.md) 참고.

## 구조

```text
yunmoon/
├── .claude-plugin/
│   ├── plugin.json          # 플러그인 매니페스트
│   └── marketplace.json     # 마켓플레이스 등록
├── skills/
│   ├── yunmoon/             # 윤문(고쳐쓰기) 스킬
│   │   ├── SKILL.md         # 오케스트레이터 (탐지·윤문·검증)
│   │   └── references/
│   │       ├── ai-tell-taxonomy.md       # 10대 카테고리 분류 (두 스킬 공유)
│   │       ├── rewriting-guide.md        # 윤문 원칙·순서·자체검증
│   │       ├── examples.md               # 장르별 before/after
│   │       ├── katfishnet-research.md    # 근거: 쉼표·POS 다양성 (KatFishNet, ACL 2025)
│   │       └── translationese-research.md # 근거: 번역투·보편소·post-editese
│   └── detect/      # 탐지(AI 작성 여부 진단) 스킬
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
[`katfishnet-research.md`](skills/yunmoon/references/katfishnet-research.md) ·
[`translationese-research.md`](skills/yunmoon/references/translationese-research.md)에 있고,
탐지·스타일로메트리·규범·선행 도구를 아우르는 **연구·참고 자료 전체 모음**은
[`docs/research.md`](docs/research.md)에 정리했다.

## 작성자

이민수 (Minsu Lee, [@amondnet](https://github.com/amondnet))

## 라이선스

[MIT](LICENSE) © 2026 Minsu Lee
