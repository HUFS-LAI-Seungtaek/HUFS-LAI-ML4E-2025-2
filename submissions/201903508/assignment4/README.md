# Assignment 4: 데이터 수집 및 탐색적 분석 (EDA) 보고서

## 1. 프로젝트 개요

프로젝트 주제: Reddit 주식 여론 분석기 (Reddit Stock Sentiment Analyzer)

목표: Reddit의 주식 관련 커뮤니티(r/stocks, r/wallstreetbets 등)에서 실시간 게시글을 수집하고, 개인 투자자들의 여론(Bullish/Bearish)을 분석하여 시각화하는 도구 개발

## 2. 데이터 수집 (Data Collection)

본 프로젝트는 Reddit의 RSS Feed를 활용하여 실시간 데이터를 수집했습니다.

수집 방법: data_collector.py 스크립트 (Python requests 라이브러리 활용)

데이터 소스: Reddit RSS Feeds (r/stocks, r/wallstreetbets, r/investing, r/StockMarket)

데이터 포맷:

  post_id: 게시글 고유 링크

  subreddit: 게시판 이름

  title: 게시글 제목

  selftext: 게시글 본문 (HTML/Text)

  created_utc: 작성 시간

파일 위치: data/reddit_stocks_live.csv

## 3. 데이터 분석 및 주요 발견 (EDA Findings)

### 3.1 기초 통계

데이터 크기: 실시간 수집된 약 100건 이상의 게시글

텍스트 길이 분포: 대부분의 게시글은 0~500자 사이의 짧은 텍스트로 구성되어 있습니다. 이는 모바일 환경에서의 뉴스 공유나 간단한 질문 글이 많기 때문으로 분석됩니다.

### 3.2 주요 발견 사항

데이터 품질 이슈: RSS Feed로 수집된 실시간 데이터는 score(좋아요)와 num_comments(댓글 수) 정보가 제공되지 않아 모두 0으로 기록됩니다. 따라서 인기도 기반 필터링보다는 최신성(Recency) 에 집중해야 함을 확인했습니다.

관심 종목(Keyword): 워드클라우드 분석 결과, Stock, Market 등의 일반 명사 외에 NVDA, TSLA, AI 등 특정 기술주 티커들이 빈번하게 등장하여 현재 시장의 관심사를 반영하고 있습니다.

텍스트 특성: r/wallstreetbets와 같은 서브레딧은 이모지(🚀, 💎)와 속어 사용 빈도가 높아, 향후 모델 학습 시 이에 대한 전처리가 중요할 것으로 판단됩니다.

## 4. 향후 계획 (Assignment 5)

모델 학습: 실시간 데이터의 라벨 부재 문제를 해결하기 위해, Kaggle 등에서 확보한 레이블링 된 과거 데이터를 활용하여 감성 분석 모델을 학습시킬 예정입니다.

서비스 적용: 학습된 모델을 본 프로젝트의 수집기(data_collector.py)와 연동하여, 실시간으로 수집되는 글의 감성을 즉시 판별해주는 파이프라인을 구축할 것입니다.
