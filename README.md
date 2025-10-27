# AI 기반 경제 뉴스 분석 웹서비스

## 프로젝트 개요
- 개발 기간: 2025.09 ~ 2025.10  
- 프로젝트 형태: 팀 프로젝트 (개인 기여 중심 백엔드 설계 및 개발)  
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
프로젝트 내에서 **백엔드 전체 구조와 데이터 흐름 설계**에 중점을 두었습니다.  
단순한 기능 구현보다는 FastAPI와 Spring Boot를 연동한 **이중 서버 구조**를 직접 구성하고,  
AI 분석 결과와 사용자 데이터가 안정적으로 교환되는 구조를 설계했습니다.  

또한, 사용자의 관심 데이터를 기반으로 하는 **회원별 개인화 추천 기능**을 구현하여  
단순 뉴스 요약 서비스가 아닌 **개인 맞춤형 경제 콘텐츠 플랫폼**으로 발전시켰습니다.

## 담당 기능
- Spring Boot 기반 웹서버 설계 및 RESTful API 구조화  
- FastAPI 분석 서버와의 데이터 통신(WebClient 활용)  
- 회원가입, 로그인, 자동 로그인 기능 구현 (세션/쿠키 기반)  
- MongoDB 기반 회원 데이터 및 선호도 저장 구조 설계  
- 회원 관심도(Explicit/Implicit) 기반 추천 기능 구현  
- 추천 API(도서·영상) 연동 및 UI 데이터 전달 구조 설계  

## 기술적 고려 및 경험
- **FastAPI ↔ Spring Boot** 간 JSON 직렬화 구조를 설계하고,  
  WebClient를 통해 AI 분석 서버 데이터를 프론트엔드로 안정적으로 전달  
- MongoDB에 사용자 정보를 **계층형 구조(JSON)** 로 저장하여,  
  이후 데이터 분석·추천 알고리즘 확장성을 고려한 DB 스키마 구성  
- GPT 기반 기사 라벨링 결과를 분석 DB에 통합하고,  
  시각화용 API를 FastAPI에서 직접 제공하도록 백엔드 역할 분리  
- 외부 API(Naver News, YouTube Data, ECOS, yFinance)를 통합하여  
  뉴스·지표·영상 데이터를 자동 갱신하는 백엔드 파이프라인 구축  
- FastAPI 서버를 Python 스케줄러(APScheduler)와 연동해  
  정기 데이터 갱신 및 MongoDB 업데이트 자동화 

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

## 개발 일정
| 기간          | 주요 작업               |
| ----------- | ------------------- |
| 9/15–9/18   | 주제 선정, 데이터 수집 테스트   |
| 9/19–10/09  | DB, 분석 파이프라인, UI 구현 |
| 10/10–10/14 | 발표 자료 제작            |
| 10/15       | 최종 발표               |
