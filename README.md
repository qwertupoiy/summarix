# 📊 AI 기반 경제 뉴스 분석 웹서비스

## 🧩 프로젝트 개요
- 개발 기간: 2025.09 ~ 2025.10  
- 프로젝트 형태: 팀 프로젝트 (개인 기여 중심 백엔드 설계 및 개발)  
- 개발 환경: Spring Boot, FastAPI, Python, MongoDB, HTML/CSS/JS  

본 프로젝트는 경제 뉴스, 유튜브 반응, 경제 지표 데이터를 통합 수집·분석하여  
사용자에게 맞춤형 경제 인사이트를 제공하는 AI 기반 웹 서비스입니다.  

저는 팀 내에서 전체 백엔드 아키텍처 설계와 데이터 흐름 구조를 주도적으로 설계하고,  
AI 분석 서버와 웹 서버를 연결하는 핵심 역할을 담당했습니다.  

## 🧠 개발 방향
프로젝트 내에서 **백엔드 전체 구조와 데이터 흐름 설계**에 중점을 두었습니다.  
단순한 기능 구현보다는 FastAPI와 Spring Boot를 연동한 **이중 서버 구조**를 직접 구성하고,  
AI 분석 결과와 사용자 데이터가 안정적으로 교환되는 구조를 설계했습니다.  

또한, 사용자의 관심 데이터를 기반으로 하는 **회원별 개인화 추천 기능**을 구현하여  
단순 뉴스 요약 서비스가 아닌 **개인 맞춤형 경제 콘텐츠 플랫폼**으로 발전시켰습니다.  

## 주요 기능
- 실시간 경제 뉴스 요약 및 감성 분석  
- 유튜브 댓글 기반 여론 감성 분석 
- GPT 기반 경제 챗봇 (뉴스 / 지표 / 환율 / 주가 응답)  
- 사용자 선호도 기반 맞춤형 추천 시스템  
- 뉴스 트렌드 / 키워드 / 감성 변화 시각화 대시보드  

## ⚙ 핵심 기여
1. 전체 아키텍처 설계 및 데이터 흐름 구조 주도  
- Spring Boot(Web) + FastAPI(AI/Data) 기반의 이중 서버 구조 설계  
- 데이터 수집 → 전처리 → 분석 → 시각화 → 추천까지 이어지는 전체 파이프라인 구조 직접 설계  
- 계층별 역할 분리로 확장성과 유지보수성을 고려한 구조 구현  
2. 개인화 추천 시스템 설계 및 구현 (핵심 기능)  
- 회원가입 시 카테고리 선호도(Explicit) 설문 시스템 설계  
- 활동 기반 선호도(Implicit) 저장 구조 설계 (확장 가능 구조)  
- MongoDB에 사용자별 선호 데이터를 계층형(JSON) 구조로 설계  
- 해당 선호도를 기반으로:  
  맞춤형 경제 도서 자동 추천  
  맞춤형 경제 영상(유튜브) 자동 추천 기능 구현  
  → 단순 정보 제공이 아닌  
  “개인 맞춤형 경제 콘텐츠 플랫폼” 구조로 확장한 핵심 기능  
3. AI 분석 서버 – 웹 서버 연동 구조 구현  
- FastAPI에서 처리된 분석 결과를 Spring Boot에서 WebClient로 통신  
- JSON 직렬화 구조 설계 및 데이터 전달 구조 통합  
- 프론트엔드는 Spring을 통해 데이터를 받아 안정적으로 시각화  
4. 외부 API 및 데이터 파이프라인 구축  
- NAVER News / YouTube / ECOS / yFinance 등 다양한 외부 API 연동  
- APScheduler를 활용하여 뉴스 및 지표 자동 갱신 구조 구현  
- 데이터 수집부터 저장까지 자동화된 파이프라인 구성  

## 기술적 고려 및 경험
- FastAPI ↔ Spring Boot 간 통신 설계를 통해 MSA 구조 경험  
- MongoDB 설계를 통해 개인화 추천을 위한 데이터 구조 설계 경험 확보  
- GPT 기반 분석 + 사용자 데이터를 결합하여  
  "AI + Personalized Service" 구조를 처음으로 구현  
- 단순 구현이 아닌, “실제 서비스 가능한 구조”를 기준으로 설계하는 시야 확장  

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
