# AI 기반 경제 뉴스 분석 웹서비스

## 프로젝트 개요
- 개발 기간: 2025.09 ~ 2025.10  
- 팀 구성: 5명 (기획 1, 백엔드 2, 데이터 분석 1, 프론트엔드 1)  
- 개발 환경: Spring Boot, FastAPI, Python, MongoDB, HTML/CSS/JS  

## 주요 기능
- 실시간 경제 뉴스 분석 및 요약  
  AI 모델이 뉴스를 수집·요약하고 주요 이슈와 감성 흐름을 시각적으로 제공  
- 유튜브 댓글 감성 분석  
  YouTube Data API를 이용해 댓글 긍·부정 비율과 주요 키워드를 시각화  
- GPT 기반 챗봇 기능  
  경제 지표, 주가, 환율, 뉴스 검색 등 질문에 실시간으로 응답  
- 개인화 추천 기능  
  사용자의 관심 분야에 따라 경제 서적 및 영상 자동 추천  
- 대시보드 시각화  
  뉴스 트렌드, 감성 추이, 키워드 랭킹 등 주요 분석 결과를 한눈에 확인 가능  

## 개발 방향
데이터 수집부터 분석, 시각화, 서비스화까지 전 과정을 직접 구현하여  
AI·데이터·웹이 통합된 서비스 구조를 구축하는 것을 목표로 하였습니다.  
팀원 간 역할을 나누기보다는 전반적인 파이프라인과 기술 구조를 함께 설계하며 협업했습니다.

## 담당 기능
- 키워드 랭킹 및 감성 분석 모듈 연동 (FastAPI → Spring Boot)  
- 회원가입 및 로그인 기능 구현 (Spring Security 미적용, 기본 세션 기반)  
- 추천 API 연동 (도서/영상 추천 페이지)  
- MongoDB 데이터 연동 및 백엔드 구조 설계  
- Spring WebClient를 활용한 FastAPI 데이터 프록시 구현  

## 기술적 고려 및 경험
- FastAPI로 AI/데이터 분석 서버를 구성하고, Spring Boot BFF 구조로 통합  
- Python 기반 데이터 전처리, TF-IDF, SBERT 임베딩, HDBSCAN 클러스터링 구현  
- MongoDB를 통한 비정형 데이터 저장 및 실시간 질의 구조 설계  
- GPT 모델 기반 감성 분석 및 주제 라벨링 자동화  
- 외부 API(Naver News, YouTube Data, ECOS, FRED, yFinance) 통합 및 데이터 자동 갱신 스케줄링 구현  

## 시연 영상
▶ [프로젝트 시연 영상 보기](https://drive.google.com/file/d/10l2G4HUBxfuKQ8xT1BKUAJbg4XiFUsp_/view?usp=drive_link)

## 대시보드 스크린샷
<img width="1000" height="1500" alt="image" src="https://github.com/user-attachments/assets/ad418c9c-9bb6-4164-97e3-4563572a9b72" />

## 데이터 소스
| 출처 | 활용 내용 | 주요 컬럼 |
|------|------------|------------|
| NAVER News API | 경제 카테고리별 뉴스 수집 | 제목, 본문, 언론사, 발행일 |
| YouTube Data API | 경제 관련 영상 댓글 및 반응 분석 | 댓글, 좋아요 수, 감성 점수 |
| ECOS API / FRED API | 경제 지표 수집 | 지표명, 수치, 단위 |
| yfinance 라이브러리 | 실시간 주가, 환율 조회 | 종목, 가격, 변동률 |

## 분석 및 시각화
| 분석 항목 | 설명 | 시각화 방식 |
|------------|------|--------------|
| 핫토픽 데이터랩 | 분야별 뉴스 언급량 추이 | 시계열 그래프 |
| 키워드 랭킹 | 기간별 주요 키워드 및 급등 단어 | 순위 리스트 |
| 감성 분석 | 긍정·부정 비율 및 감성 변화 추이 | 게이지 그래프 |
| 오피니언 마이닝 | 유튜브 댓글 기반 감성 분석 | 파이차트, 워드클라우드 |
| 기사 클러스터링 | GPT 기반 주제 라벨링 | 트리맵 시각화 |

## 웹 구성
### 대시보드
- 실시간 글로벌 경제 속보  
- 주요 키워드 및 감성 요약  
- 기사 수, 긍·부정 추이 그래프  
- 유사 기사 그룹 및 클러스터 표시  

### 뉴스 요약
- 금일 주요 뉴스 및 핵심 키워드 요약  

### 유튜브 분석
- 댓글 감성 비율, 워드클라우드 시각화  

### 챗봇
- GPT 기반 대화형 경제 챗봇  
- STT/TTS 지원 (CLOVA, Google Cloud)  

### 추천 및 회원 기능
- 관심 분야 기반 도서/영상 추천  
- 회원가입, 로그인, 선호도 반영  

## 기술 스택
| 구분 | 기술 |
|------|------|
| Frontend | HTML, CSS, JavaScript, ToastUI Chart |
| Backend (Web) | Spring Boot (Java 17, Gradle 8.x) |
| Backend (AI/Data) | FastAPI, Python 3.10+, pandas, transformers |
| DB | MongoDB Atlas |
| AI | OpenAI GPT-5, KoBART Summarizer, Custom Sentiment Dict |
| Infra | APScheduler, Google TTS, CLOVA STT |

## 폴더 구조
```
│
├── ① [수집 계층: Collect]
│     ├─  news_clawler.py        → 네이버 경제 뉴스 수집
│     ├─  youtube_crowler.py     → 유튜브 영상·댓글 수집
│     └─  MongoDB(test123)
│          ├─ shared_articles
│          ├─ youtube_db2
│          └─ youtube_comments
│
├── ② [전처리 계층: Preprocessing]
│     ├─ preprocess_pipeline_1.py
│     │    ├─ 텍스트 정제 / 불용어 제거(stopwords.txt)
│     │    ├─ TF-IDF + SBERT 임베딩
│     │    └─ 차원 축소(SVD) 후 저장
│     └─ 결과 → MongoDB(articles_preprocessed)
│
├── ③ [분석·클러스터링 계층: Analysis & Clustering]
│     ├─ cluster_pipeline_3.py     → UMAP + HDBSCAN 군집화
│     ├─ summarize.py              → 대표 기사·키워드 요약
│     ├─ label_gpt.py              → GPT 기반 이슈명(Label) 생성
│     ├─ attach_clusters_to_articles_2.py → 기사-클러스터 매핑
│     └─ 결과 → MongoDB(clusters)
│
├── ④ [트렌드·통계 계층: Trend & Statistics Layer]
│     ├─ emoa.py            → 감정 평균 변화 추이
│     ├─ headline.py        → 실시간 경제 헤드라인
│     ├─ count.py           → 카테고리별 뉴스 수량
│     ├─ category_trends.py → 네이버 데이터랩 검색 트렌드
│     └─ config.py          → API 키·카테고리 매핑 설정
│
├── ⑤ [추천 계층: Recommendation Layer]
│     ├─ youtube_api.py     → YouTube 영상 추천 (v3 API)
│     ├─ books_api.py       → 알라딘 도서 추천
│     ├─ book_db_save.py    → 추천 결과 DB 저장
│     └─ client.html        → 도서/영상 카드 UI
│
├── ⑥ [대시보드 계층: Visualization Layer]
│     ├─ senti_chart.py     → 감정 분포 그래프용 API
│     ├─ keywords.py        → 일간 키워드 Top-N
│     ├─ main.py            → FastAPI 템플릿 라우터
│     ├─ index.html         → Chart.js + WordCloud2.js UI
│     └─ index.js           → fetch + 렌더링 로직
│
├── ⑦ [AI 챗봇 계층: AI Assistant Layer]
│     ├─ chatbot.py
│     │    ├─ GPT-5 Function Calling
│     │    ├─ get_latest_news / get_indicator / get_market / search_docs
│     │    ├─ FRED, ECOS, yFinance, MongoDB, Vector Store 연동
│     ├─ watcher.py
│     │    └─ docs 폴더 실시간 감시 → RAG 문서 자동 업로드
│     └─ .vector_store_id, .vs_state.json → RAG 인덱스 상태
│     │ 
│     └─ chatbot_rag.py
│
├── ⑧ [Spring Boot BFF 계층: Backend For Frontend Layer]
│     ├─ Controller
│     │    ├─ YoutubeController.java  → FastAPI(8008)/videos 프록시
│     │    └─ AnalysisController.java → FastAPI(8008)/analysis 프록시
│     ├─ DTO
│     │    ├─ VideoDetailDto.java
│     │    ├─ VideoSummaryDto.java
│     │    ├─ AnalysisResponseDto.java
│     │    ├─ CommentItem.java
│     │    └─ WordItem.java
│     ├─ Domain
│     │    ├─ VideoDoc.java
│     │    └─ CommentDoc.java
│     └─ WebClient → FastAPI JSON 직렬화 후 프론트 전달
│
├── ⑨ [프론트엔드 계층: Dashboard & Interaction]
│     ├─ Thymeleaf 템플릿
│     │    └─ pages/youtube_opinion.html, dashboard.html 등
│     ├─ JS 모듈
│     │    ├─ sentiment.js / ticker.js / trands.js / emoa.js
│     │    └─ wordcloud2.js (시각화)
│     └─ Chart.js, Fetch API로 Spring `/api/...` 호출
│
└── ⑩ [데이터 저장소: MongoDB + OpenAI Vector Store]
      ├─ MongoDB Atlas
      │    ├─ shared_articles, youtube_db2, clusters, ...
      └─ OpenAI Vector Store (docs 기반 RAG 검색)
```

## 환경 변수 (.env 예시)
```env
ECOS_API_KEY=xxxx
OPENAI_API_KEY=sk-xxxx
NAVER_CLIENT_ID=xxxx
NAVER_CLIENT_SECRET=xxxx
GOOGLE_APPLICATION_CREDENTIALS=./credentials.json
MONGO_URI=mongodb+srv://Dgict_TeamB:team0000@cluster0.mongodb.net/
```

## 팀 역할
| 이름  | 담당 업무                |
| --- | -------------------- |
| 유승민 | 기획, 운영, 챗봇           |
| 유도현 | 백엔드, 키워드 랭킹, 추천, 로그인 |
| 윤유정 | 글로벌 뉴스, 감성 요약, 기사 통계 |
| 장성진 | 크롤러, 뉴스 요약, 오피니언 마이닝 |
| 정수현 | 프론트엔드 UI/UX 설계 및 구현  |

## 개발 일정
| 기간          | 주요 작업               |
| ----------- | ------------------- |
| 9/15–9/18   | 주제 선정, 데이터 수집 테스트   |
| 9/19–10/09  | DB, 분석 파이프라인, UI 구현 |
| 10/10–10/14 | 발표 자료 제작            |
| 10/15       | 최종 발표               |
