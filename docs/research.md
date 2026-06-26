# 윤문(yoonmoon) 연구·참고 자료 모음

윤문의 학술·실무 토대를 정리한 큐레이션 문헌목록이다. 한국어 AI 텍스트 탐지, AI 글의 문체적 특징,
번역투·post-editese, 한국어 글쓰기 규범·선행 도구를 다룬다.

> **검증 방법.** 각 출처는 WebSearch로 발굴한 뒤 ACL Anthology · arXiv · KCI · DBpia · 국립국어원 등
> 원 페이지를 실제로 열어 서지를 확인했고, 핵심 URL은 HTTP 상태(200)로 생존을 재확인했다.
> 저자·연도·수치는 추측하지 않았다. confidence: **HIGH**(원문/서지 확인) · **MED**(2차 교차확인) · **LOW**(미확인).
> 미확인 항목은 §8에 따로 모았다.

> **스킬에 직접 반영된 근거 문서**(이 모음의 부분집합이자 taxonomy가 인용):
>
> - [`skills/humanize/references/katfishnet-research.md`](../skills/humanize/references/katfishnet-research.md) — 쉼표·POS 다양성 (카테고리 4·9)
> - [`skills/translate-polish/references/translationese-research.md`](../skills/translate-polish/references/translationese-research.md) — 번역투·보편소·post-editese (translate-polish 본거지, humanize 카테고리 1·2·6 공유)

## 목차

1. [한국어 AI/LLM 텍스트 탐지](#1-한국어-aillm-텍스트-탐지)
2. [AI 글의 문체적 특징·스타일로메트리](#2-ai-글의-문체적-특징스타일로메트리)
3. [AI 텍스트 탐지 기법·워터마킹](#3-ai-텍스트-탐지-기법워터마킹)
4. [번역투·번역 보편소·post-editese](#4-번역투번역-보편소post-editese)
5. [한국어 글쓰기 규범·교정 가이드](#5-한국어-글쓰기-규범교정-가이드)
6. [선행 도구 (prior art)](#6-선행-도구-prior-art)
7. [한국어 NLP 툴링](#7-한국어-nlp-툴링)
8. [윤문 시사점 · 미확인 항목](#8-윤문-시사점--미확인-항목)

---

## 1. 한국어 AI/LLM 텍스트 탐지

| 자료                                                                                                                                                                                                                                            | 저자/연도/발표처                              | 핵심                                                                                                                                                                                    | 윤문 관련성                                                                | conf                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ---------------------- |
| **KatFishNet** — Detecting LLM-Generated Korean Text through Linguistic Feature Analysis · [ACL](https://aclanthology.org/2025.acl-long.1030/) · [arXiv](https://arxiv.org/abs/2503.00032) · [code](https://github.com/Shinwoo-Park/katfishnet) | Park, Kim, Kim, Han / 2025 / ACL Main         | 한국어 LLM 텍스트 탐지 **최초 벤치마크**(KatFish, 3장르). 신호 = 띄어쓰기·**POS n-gram 다양성**·**쉼표 사용**. 기존 최선 대비 +19.78% AUROC                                             | 탐지·taxonomy의 1순위 근거 → `katfishnet-research.md`                      | HIGH                   |
| **XDAC** — XAI-Driven Detection and Attribution of LLM-Generated News Comments in Korean · [ACL](https://aclanthology.org/2025.acl-long.1108/) · [code](https://github.com/airobotlab/XDAC)                                                     | Go, Kim, Oh, Kim (KAIST 등) / 2025 / ACL Main | 한국어 **댓글(단문)** 탐지·귀속. AI=격식·정형·**표준화**, 사람=줄바꿈·이중공백·반복문자(ㅋㅋ). **이모지는 유무가 아니라 표준화 정도가 신호**. 탐지 F1 98.5%·귀속 84.3%                  | 단문/구어체 신호 — KatFishNet(문어체) 보완, detect 스킬에 "SNS/댓글 톤" 축 | HIGH                   |
| **LREAD** — Rubric-Based Expert-Panel Study of Human Detection of LLM-Generated Korean Text · [arXiv 2601.19913](https://arxiv.org/abs/2601.19913) · [code](https://github.com/Shinwoo-Park/lread)                                              | Park, Han (Yonsei) / 2026 preprint            | 사람 판별: 직관 F1 0.60 → **루브릭 적용 시 0.90**(Fleiss κ −0.09→0.24→0.82, 3단계). "표면적 매끄러움"이 사람을 오도. 루브릭 차원 = 자연스러운 한국어 표현·register 안정성·연결어/구두점 | detect 스킬의 **사람 검수 루브릭** 직접 근거. KatFishNet 후속(동일 연구진) | HIGH·검증완료(2026-06) |
| 인간의 글과 ChatGPT의 글에 대한 텍스트언어학적 접근 (TOPIK 쓰기) · [KCI](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART003070390)                                                     | 조신(Zhao Xin) / 2024 / 언어와 정보 사회 51   | 사람 vs ChatGPT 작문을 상위·거시·미시구조·결속성/응집성으로 대조(질적)                                                                                                                  | 한국어 작문의 담화 구조 차이 → 윤문 리듬·결속 규칙 토대                    | HIGH                   |
| 챗GPT 이후 기계·인간 번역 문체 차이 변화 · [KCI](https://www.kci.go.kr/kciportal/landing/article.kci?arti_id=ART003000086)                                                                                                                      | 이창수 / 2023 / 번역학연구 24(3)              | Biber 67자질 PCA. **ChatGPT는 격식·문어체 편향**으로 뚜렷이 분기, 자가교정에도 문체 거의 불변                                                                                           | "AI=격식·문어체 편향" 가설의 정량 근거                                     | HIGH                   |

> **다국어 MGT 벤치마크에 한국어 없음** (각 논문 언어표 직접 확인): MULTITuDE([2310.13606](https://arxiv.org/abs/2310.13606), 11개 언어), M4GT-Bench([2402.11175](https://arxiv.org/abs/2402.11175)), M4([EACL](https://aclanthology.org/2024.eacl-long.83/)), MultiSocial([2406.12549](https://arxiv.org/abs/2406.12549)), RAID([2405.07940](https://arxiv.org/abs/2405.07940), 영어중심). → 한국어는 사실상 **KatFish가 유일 전용 리소스**. 이 공백이 윤문의 차별점.

---

## 2. AI 글의 문체적 특징·스타일로메트리

| 자료                                                                                                                                    | 저자/연도/발표처                      | 핵심                                                                                                    | 한국어 적용 주의                                                                                          | conf |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ---- |
| Delving into LLM-assisted writing — excess vocabulary · [arXiv 2406.07016](https://arxiv.org/abs/2406.07016)                            | Kobak 외 / 2024→Science Advances 2025 | PubMed 1,500만+ 분석. LLM 등장 후 style words(delve, intricate…) 급증. 2024년 초록 ~13.5% LLM 처리 추정 | 단어 리스트는 **영어 전용**. _방법론_(빈도 초과분)만 한국어로 차용                                        | HIGH |
| Why Does ChatGPT "Delve" So Much? · [arXiv 2412.11385](https://arxiv.org/abs/2412.11385)                                                | Juzek, Ward / 2024→COLING 2025        | 21개 과대표현 단어. 원인은 **RLHF 유력**(미확정)                                                        | "한국어 LLM도 선호 토큰 과사용" 가설의 근거                                                               | HIGH |
| Monitoring AI-Modified Content at Scale (peer reviews) · [arXiv 2403.07183](https://arxiv.org/abs/2403.07183)                           | Liang 외 / 2024 / ICML                | 코퍼스 수준 분포이동으로 6.5–16.9% LLM 수정 추정. 라벨 불필요                                           | 코퍼스-레벨 탐지 아키텍처는 언어 무관 → 한국어 적용 가능                                                  | HIGH |
| Detection and Measurement of Syntactic Templates in Generated Text · [EMNLP 2024](https://aclanthology.org/2024.emnlp-main.368/)        | Shaib 외 / 2024                       | LLM은 POS 시퀀스 "템플릿" 과반복 → 통사적으로 더 균질                                                   | "AI=반복 통사 템플릿" 신호. **단 KatFishNet은 한국어서 AI의 POS 다양성↑를 보고** → 부호는 KatFishNet 기준 | HIGH |
| Playing with Words: Vocabulary & Lexical Richness of ChatGPT vs Humans · [arXiv 2308.07462](https://arxiv.org/abs/2308.07462)           | Reviriego 외 / 2023                   | AI는 어휘 다양성·풍부도 낮음                                                                            | TTR은 교착어라 **형태소/원형 토큰화 후** 계산 필수                                                        | HIGH |
| Stylometry recognizes human and LLM texts in short samples · [arXiv 2507.00838](https://arxiv.org/abs/2507.00838)                       | Przystalski 외 / 2025                 | 트리 분류기가 ~10문장 단편서도 인간 vs GPT-4 최대 .98                                                   | 짧은 입력서도 작동(문단 윤문에 유리). 한국어 태거 필요                                                    | HIGH |
| Stylometry can reveal AI authorship in Japanese · [PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0335369) | Zaitsu 외 / 2025                      | 일본어서 통합 스타일로메트리 ~99.8%. **Mecab + 의존파서** 사용                                          | 교착어 선례 — 한국어도 Mecab-ko/KoNLPy+파서 필요                                                          | HIGH |
| A Survey of AI-generated Text Forensic Systems · [arXiv 2403.01152](https://arxiv.org/abs/2403.01152)                                   | Kumarage 외 / 2024                    | 탐지/귀속/특성화 taxonomy 지도                                                                          | 어떤 특징이 있는지 개관                                                                                   | HIGH |

**비학술(분석글·벤더, 명시):** Reuters Institute "How AI-generated prose diverges"([link](https://reutersinstitute.politics.ox.ac.uk/news/how-ai-generated-prose-diverges-human-writing-and-why-it-matters), 2025), The Conversation "Too many em dashes…"(Kreuz, 2025) — tell 카탈로그이나 **단일 tell은 비결정적**·대부분 영어 전용. GPTZero "Perplexity and Burstiness"([link](https://gptzero.me/news/perplexity-and-burstiness-what-is-it/)) — burstiness 개념은 한국어 전이되나 신뢰성은 논쟁적.

---

## 3. AI 텍스트 탐지 기법·워터마킹

| 기법                                                                                                                                                                                                                           | 저자/연도                   | 아이디어                                                       | 한계(윤문 관점)                                                                      | conf       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ---------- |
| **GLTR** · [ACL 2019](https://aclanthology.org/P19-3019/)                                                                                                                                                                      | Gehrmann 외 / 2019          | 토큰별 LM 확률·순위 시각화(생성문=고확률 토큰 과다)            | 샘플링·모델 발전에 약화. 언어별 캘리브레이션 필요                                    | HIGH       |
| **DetectGPT** · [arXiv 2301.11305](https://arxiv.org/abs/2301.11305)                                                                                                                                                           | Mitchell 외 / 2023 / ICML   | log-prob 곡률. zero-shot, 분류기 불필요                        | **화이트박스**(log-prob 접근), **패러프레이즈 시 붕괴**. 한국어 가능 스코어 LLM 필요 | HIGH       |
| **Binoculars** · [arXiv 2401.12070](https://arxiv.org/abs/2401.12070)                                                                                                                                                          | Hans 외 / 2024 / ICML       | perplexity ÷ cross-perplexity. zero-shot, 학습 불필요          | 강한 수치는 영어 중심. 한국어·편집 텍스트 미검증                                     | HIGH       |
| **Ghostbuster** · [arXiv 2305.15047](https://arxiv.org/abs/2305.15047) · [NAACL](https://aclanthology.org/2024.naacl-long.95/)                                                                                                 | Verma 외 / 2024 / NAACL     | 약한 LM 확률특징 조합 + 분류기. 블랙박스 친화                  | **비원어민 영어서 신뢰도 저하 명시** → 한국어 작성/번역 텍스트 위양성 위험           | HIGH       |
| **GPTZero** · [gptzero.me](https://gptzero.me/)                                                                                                                                                                                | Tian, Cui / 2023 / 상용     | perplexity+burstiness+문체 결합                                | 짧은 입력·비원어민서 **위양성** 다수 보도. 한국어 미검증                             | HIGH(도구) |
| **무하유 GPTKiller** · [copykiller.com/gptkiller](https://www.copykiller.com/gptkiller)                                                                                                                                        | 무하유 / 2023 / 상용        | 국내 최초 한국어 학습 DetectGPT 표방. 문서/문단/문장 AI 작성률 | 윤문의 **적대적 레퍼런스**(회피 도구로 포지셔닝 금지). 정확도 미공개                 | HIGH(도구) |
| **Watermarking** · Kirchenbauer 외 [2301.10226](https://arxiv.org/abs/2301.10226)·[2306.04634](https://arxiv.org/abs/2306.04634), SynthID-Text(DeepMind, Nature 2024, [code](https://github.com/google-deepmind/synthid-text)) | 2023–24                     | green-list 편향 등 생성기측 표식                               | **생성기 협조 전제** → 임의 한국어 텍스트 탐지 부적합                                | HIGH       |
| **Paraphrasing evades detectors (DIPPER)** · [arXiv 2303.13408](https://arxiv.org/abs/2303.13408)                                                                                                                              | Krishna 외 / 2023 / NeurIPS | 패러프레이징이 watermark·GPTZero·DetectGPT 회피                | **직접 중요**: 윤문=패러프레이즈형 변환이라 watermark/탐지 신호가 제거됨을 입증      | HIGH       |

---

## 4. 번역투·번역 보편소·post-editese

상세 정리·서지는 스킬 레퍼런스 [`translationese-research.md`](../skills/translate-polish/references/translationese-research.md) 참조.
핵심만:

- **한국어 번역투 유형론** — 김정우(2007, 정전), 김도훈(2009, 직역 대명사·무생물 '-들'·무생물 주어), 이영옥(2001)/최서영(2022, 무생물 주어+타동사), 오경순(2010)/최유숙(2023, 피동·이중피동), 전영철(2015, '-들' 의미론), 국립국어원 『새국어생활』 2012 번역 특집.
- **번역 보편소** — Baker(1993; 1996: 단순화·명시화·규범화·평준화), Toury(1995: 규범화·간섭 법칙), Laviosa(1998/2002), Chesterman(2004: S-/T-universals — 윤문은 결과만 보므로 **T-universals**), Pym(2008, 위험회피 통합).
- **post-editese / MT translationese** — Toral(2019, "악화된 번역투"), Vanmassenhove 외(2019/2021, 어휘 다양성 손실), Kong & Macken(2025, EN-ZH: 짧은 문장·역접 접속사 과다), Jalota 외(2023, 병렬데이터 없이 번역투 제거).
- **한국어 MT 품질평가** — **Park & Padó(LREC-COLING 2024)**: fluency 차원에 "Unnaturalness" 오류 명시 코딩(가장 직접적 공학 근거), 최희경(2016), 안미영(2020), NIA/AI Hub MQM/SQM 자원.

### 추가 검증 1차 문헌 — 명사화·관형절 통사 표지 (2026-06 발굴)

§8 taxonomy gap(명사화·관형절 중첩)을 메우기 위해 새로 발굴·검증한 한국어 1차 문헌. 모두 KCI/DBpia 원 페이지로 서지 확인(핵심 2건은 본 세션에서 재검증).

| 자료                                                                                                                                                                                           | 저자/연도/발표처                           | 핵심                                                                              | 윤문 매핑                                             | conf |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------- | ----------------------------------------------------- | ---- |
| 국어 문법적 은유에 대한 체계기능언어학적 접근 · [DBpia](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE08849360)                                                                     | 정려란 / 2018 / 한국어문교육 26            | 한국어 명사화=문법적 은유, 학술·격식 텍스트의 정보밀도·객관 문체 자원(SFL)        | **카테고리 6 명사화 1순위 근거**(Baker 간접근거 대체) | HIGH |
| 과학 교과서의 '문법적 은유'를 중심으로 본 국어과의 도구 교과적 본질 · [KCI](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002237542) | 소지영·주세형 / 2017 / 국어교육연구 39     | 명사화가 고학년·학술 텍스트일수록 증가 → 정보밀도·객관·중립 문체, register 의존   | 명사화 과잉=문어·격식 지표("AI=격식편향"과 직결)      | HIGH |
| 명사 수식 구문의 번역 글쓰기 문제 · [KCI](https://www.kci.go.kr/kciportal/landing/article.kci?arti_id=ART001623231)                                                                            | 김혜영 / 2011 / 돈암어문학 24(89–120)      | 영한 명사 수식: 영어 어순·관형격 '의' 반복·다중 내포 → 번역투, 용인성·가독성 저하 | 카테고리 1(관형절 중첩)·6(관형격 남발) 직접 근거      | HIGH |
| 번역서와 비번역서의 문장·절 길이 비교(아동 번역서) · [KCI](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART001559668)                  | 성승은 / 2011 / 번역학연구 12(2)           | 번역서가 비번역서보다 **더 긴 문장·더 긴 관형절(determinative clauses)**          | "번역투=긴 관형 수식"의 계량 직접 증거                | HIGH |
| 관형사절의 한영 기계번역을 위한 복합문 분절 · [DBpia](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE01513519)                                                                       | 정경미 / 2010 / 우리말글 49                | 관형사절 복합문 → 단문 분절·복원                                                  | 윤문 교정전략('절 끊어 분할')의 처리부담 근거         | HIGH |
| 관형절의 한영 번역 기법 · [KCI](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002073616)                                             | 박옥수 / 2015 / 동아인문학 33              | 한국어 관형절(좌분지) ↔ 영어 형용사절(우분지) 비대칭·번역기법 6종                 | 좌/우분지 전환 = 번역투 발생점                        | HIGH |
| 영어와 한국어의 명사화에 관한 비교 연구 · [DBpia](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE01236514)                                                                           | 박기성 / 2009 / 새한영어영문학 51(3)       | 영·한 명사화 대조, 양 언어서 grammatical metaphor 장치                            | 영한 명사화 대조 이론 토대(보조)                      | HIGH |
| Challenging stereotypes about academic writing · [PDF](https://jan.ucc.nau.edu/biber/Biber/Biber_Gray_2010.pdf)                                                                                | Biber & Gray / 2010 / JEAP 9(1)            | 학술 문어는 절 확장이 아닌 **명사화·명사구 압축**으로 복잡화                      | 명사화=문어 표지의 영어권 정설(방법론)                | HIGH |
| Syntactic Comprehension of RC & Center Embedding · [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC7226570/) · DOI 10.3390/brainsci10040202                                                     | Cheon 외 / 2020 / Brain Sciences 10(4):202 | 한국어 화자: 이중 내포 이해 정확도 62.75%로 급락(단 RC+CE 결합 촉진 효과도)       | 중첩 처리부담 실험 근거(nuance 필요)                  | HIGH |

> **반대 증거(균형 — 과교정 방지).** 구민지·양길석(2013, 이중언어학 52, [KCI](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART001778743)): 한국어 읽기 난이도에서 **'문장 길이' 요인은 통계적으로 유의하지 않았다**(어휘 난이도가 지배적). 또 한국어는 좌분지 SOV라 단일 관형절은 자연스럽다(Cheon 외 2020도 RC+CE 결합 시 촉진 효과 보고). → 이 신호는 '관형절 개수·길이' 임계치가 아니라 **번역투 구조(영어 어순 모사·'의' 반복·다중 내포로 인한 중의성)**로 정의해야 위양성을 피한다. 김혜영(2011)이 정확히 이 프레임(구조적 문제 → 용인성·가독성)을 제공.

---

## 5. 한국어 글쓰기 규범·교정 가이드

**규범 자료 (국립국어원 / 문체부)**

| 자료                                                          | URL                                                                                 | 윤문 활용                             | conf |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------- | ---- |
| 표준국어대사전                                                | https://stdict.korean.go.kr/                                                        | 어휘 표준 표기/뜻 1차 검증            | HIGH |
| 어문 규범 통합 포털(맞춤법·표준어·외래어·로마자)              | https://korean.go.kr/kornorms/example/exampleList.do                                | 맞춤법·띄어쓰기·외래어 표기 근거 조문 | MED  |
| 한글 맞춤법·표준어 규정 해설(2018)                            | https://www.korean.go.kr/front/reportData/reportDataView.do?mn_id=45&report_seq=944 | 경계 사례 유권해석                    | HIGH |
| 「공공언어 바로 쓰기(개정판)」 — **일본어 투 용어 50개** 포함 | https://www.korean.go.kr/front/etcData/etcDataView.do?etc_seq=699                   | 일본어투 치환 사전·간결화 규칙        | HIGH |
| 「쉬운 공문서 쓰기 길잡이(2022)」                             | https://www.korean.go.kr/front/etcData/etcDataView.do?etc_seq=700                   | 피동 줄이기·명사 나열 풀기            | HIGH |
| 우리말 다듬기(말터)                                           | https://www.korean.go.kr/front/imprv/refineList.do                                  | 외래어→순화어 치환                    | MED  |
| 온라인가나다 Q&A                                              | https://www.korean.go.kr/front/onlineQna/onlineQnaList.do?mn_id=216                 | 애매한 용법 공식 사례                 | HIGH |
| 『새국어생활』 2012 "번역과 국어" 특집                        | https://www.korean.go.kr/nkview/nklife/2012_1/22_01.pdf                             | 번역투 유형 분류 학술 근거            | HIGH |

> **URL 정정·브라우저 검증(2026-06).** 어문 규범 통합 포털·우리말 다듬기(말터)의 기존 서브도메인(`kornorms.korean.go.kr`·`malteo.korean.go.kr`)은 이 환경 DNS에서 해석되지 않아, 해석되는 경로형(`korean.go.kr/kornorms/…`·`www.korean.go.kr/front/imprv/refineList.do`)으로 정정했다. Orca 내장 브라우저로 본문(외래어 표기 용례·다듬은 말 18,309건)을 직접 확인 → 두 자료 **MED→HIGH**.

**교정 가이드·서적**

| 서적                                 | 저자 / 출판          | 영역                                                | conf |
| ------------------------------------ | -------------------- | --------------------------------------------------- | ---- |
| 『우리글 바로쓰기』(전5권)           | 이오덕 / 한길사      | 일본어·서양 번역투 → 토박이말                       | HIGH |
| 『이수열 선생님의 우리말 바로 쓰기』 | 이수열 / 현암사 2014 | 항목별 치환표                                       | HIGH |
| 『번역투의 유혹』                    | 오경순 / 이학사      | **일본어투** 전문('~적', 'の'→'의', 이중피동)       | HIGH |
| 『번역의 탄생』                      | 이희재 / 교양인      | **영어 번역투** 전문(무생물 주어·명사화·'~들'·수동) | HIGH |

---

## 6. 선행 도구 (prior art)

| 도구                             | URL                                     | 무엇                                                                                                      | 윤문 관점                                                    | conf       |
| -------------------------------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | ---------- |
| **epoko77-ai/im-not-ai** ★       | https://github.com/epoko77-ai/im-not-ai | 한국어 AI 글→사람 글 윤문(번역투·문체). Claude/Codex 스킬. 10대 A~J taxonomy + 심각도 S1~S3 + Fast/Strict | 가장 직접적 청사진(개념 참고). 윤문은 독자 taxonomy로 재작성 | HIGH       |
| 부산대 한국어 맞춤법/문법 검사기 | http://speller.cs.pusan.ac.kr/          | 국내 권위 맞춤법·문법 엔진                                                                                | "1차 정확성 레이어" 참고(문체·AI 티는 비대상)                | HIGH(기능) |
| 네이버 맞춤법 검사기             | search.naver.com 내                     | 맞춤법·띄어쓰기(최대 500자)                                                                               | 경량 교정 비교군                                             | HIGH(기능) |
| 카피킬러/GPTKiller               | https://www.copykiller.com/             | 표절 + AI 탐지                                                                                            | 탐지 적대 레퍼런스                                           | HIGH       |
| 워드바이스 AI 휴머나이저         | https://wordvice.ai/tools/ai-humanizer  | 47개 언어 패턴 치환, "탐지 통과 보장 못 함" 명시                                                          | 휴머나이저 경쟁군                                            | HIGH       |
| py-hanspell                      | https://github.com/ssut/py-hanspell     | 네이버 검사기 비공식 API 래퍼                                                                             | 외부 검사기 래핑의 취약성 반례                               | HIGH       |

---

## 7. 한국어 NLP 툴링

- **KoNLPy / Mecab-ko** — https://konlpy.org/ — 형태소 분석·POS 태깅. KatFishNet식 특징(POS n-gram 다양성·형태소 단위 TTR·띄어쓰기 분석)을 한국어 텍스트에 계량할 때 표준 툴체인. conf HIGH.
- **KLUE: Korean Language Understanding Evaluation** — [arXiv 2105.09680](https://arxiv.org/abs/2105.09680) — 8개 한국어 NLU 과제(NER·의존파싱 포함) + KLUE-BERT/RoBERTa. 통사 기반 스타일로메트리 특징에 활용. conf HIGH.

---

## 8. 윤문 시사점 · 미확인 항목

### 시사점 — 한국어에 그대로 적용하면 안 되는 것 (영어 전용 tell)

- **특정 영어 단어 리스트**("delve" 등)·**em-dash 남용**·**축약형/수동태 회피**·**영어식 hedging 어구**("often") → 한국어는 `-것 같다/-수 있다` 등 어미로 실현. 한국어 excess-vocabulary 리스트는 코퍼스로 **새로 산출**해야 함(방법론만 차용).
- **TTR·POS n-gram** → 교착어라 **형태소/원형 토큰화 후** 계산 필수. 또 POS 다양성의 *방향*은 영어 연구(AI=균질)와 반대로 **KatFishNet 기준(한국어 AI=POS 다양성↑·쉼표 과용)** 을 채택.
- **watermark 계열** → 생성기 협조 전제라 임의 한국어 텍스트엔 무관, 윤문(패러프레이즈)이 신호 제거.

### taxonomy 보강 여지 (현재 gap)

- **명사화·관형절 중첩** — 1차 문헌 **확보(2026-06)**: 명사화는 정려란(2018)·소지영·주세형(2017)의 문법적 은유·SFL 연구, 관형절 중첩은 김혜영(2011)·성승은(2011)으로 직접 근거 마련(§4 "추가 검증 1차 문헌" 표). 단 **경동사 분리('활용을 하다'·한자어 대동사 '실시·수행·진행하다')를 번역투/AI 티로 규정한 peer-review 학술 1차 문헌은 재조사(2026-06)에도 미발굴** — 한성어문학 2020(임형모, 'about' 전치사 전담)은 부합 안 하고, 대동사 학술 문헌은 순수 통사·의미론(논항구조)뿐. 다만 홍성호(2020, 한국경제 생글생글 [「서술어 3종 세트」](https://sgsg.hankyung.com/article/2020061958541))가 '명사+을 실시·진행·수행하다'를 한자어 대동사 군더더기로 보고 '명사+하다' 간결화를 권고(비학술·권위 칼럼), 이오덕·이수열 글쓰기서·국립국어원 공공언어 가이드(§5)와 함께 처방 근거가 된다.
- detect 스킬: **LREAD 루브릭**(내용·조직·표현 3대 차원 + fluency trap)을 [`skills/detect/references/lread-rubric.md`](../skills/detect/references/lread-rubric.md)로 **반영 완료**. XDAC의 **단문/SNS 신호** 축은 **검증 완료(2026-06)** — XDAC(ACL `2025.acl-long.1108`) 본문 대조로 신호(반복문자·줄바꿈·이중공백 _부재_ 등)·수치 확정, [`xdac-research.md`](../skills/detect/references/xdac-research.md)에 정리. **detect 스킬 반영 완료** — Phase 0 단문/SNS 게이트 + 조건부 Phase 1-S(단문 장르 게이트 + 다축 합산, "이모지=사람" 단정 금지, 카테고리 8과 신호 방향 반대 처리)로 통합.

### 미확인 (인용 전 추가 검증 필요)

- **이근희(2005)** 『이근희의 번역 산책: 번역투에서 번역의 전략까지』(한국문화사, 2005) — 다수 2차 인용 교차확인으로 **단행본 서지 확정(MED)**, 1차 페이지 미열람. / 정영옥(2010), 최정아(2003) — 2차 인용만, 서지 미확인 (LOW)
- **류현주(2009) "번역투와 번역자투"**(번역학연구 10(2):7–22) — 2차 서지 교차확인(김한식 2012 참고문헌)으로 **MED 격상**
- Pym(2008) 페이지/DOI(Benjamins 403 차단), Baker(1996) 보편소별 정확 페이지 — 1차 미열람 (MED)
- **미검증 arXiv ID** — 검색 요약에서 환각 가능성이 있는 ID는 원 페이지로 실재 확인 전 **인용 금지**. (초안에선 26xx를 "미래 날짜형"으로 분류했으나 현재 2026-06 기준 2602.x~2606.x는 이미 과거 — 판단 기준은 '날짜'가 아니라 '실재 검증 여부'다.) **LREAD `2601.19913`은 2026-06 검증 완료**(arXiv v1~v3 페이지·GitHub `Shinwoo-Park/lread` 실재 확인, 제목·수치·루브릭 배점 본문 대조) → 인용 가능. 로컬 아카이브: [`docs/papers/LREAD-2601.19913v3.pdf`](papers/LREAD-2601.19913v3.pdf) (Git LFS)
- HCLT/KIISE 내 한국어 AI 생성문 탐지 논문 — **HCLT 2023 "생성형 AI가 생성한 문서를 탐지하는 판별기에 대한 연구" 발표 확인**(뉴스·블로그 교차, MED). 정확 서지(저자·페이지)는 koreascience.kr 추가 확인 필요
- 국립국어원 **어문 규범·우리말 다듬기 — 브라우저 검증 완료(2026-06)**: 기존 서브도메인(`kornorms`·`malteo.korean.go.kr`)이 이 환경 DNS에서 미해석 → 경로형으로 정정하고 Orca 내장 브라우저로 본문 직접 확인(§5 MED→HIGH).

---

_최종 갱신: 2026-06. 검증된 출처만 수록했으며, LLM 발전에 따라 주기적 갱신을 권장한다._
