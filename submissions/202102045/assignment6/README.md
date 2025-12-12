# 📢 외교부 소식 자동 요약 서비스 (MOFA News Summarizer)

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?logo=streamlit&logoColor=white)
![Model](https://img.shields.io/badge/Model-KoBART-orange)

**"복잡한 국제 정세와 외교 소식, AI가 3줄로 핵심만 요약해 드립니다."**

</div>

---

## 📖 프로젝트 개요

**MOFA News Summarizer**는 정보 과잉(Information Overload) 시대에 외교 관련 소식을 빠르고 정확하게 파악하기 위해 개발된 **AI 뉴스 요약 서비스**입니다.

사용자가 긴 보도자료를 다 읽지 않아도 **AI가 핵심 내용을 3줄로 요약**해 주며, 외교부 공식 블로그의 최신 글을 자동으로 수집하여 실시간 동향을 한눈에 제공합니다. 별도의 설치 없이 웹 브라우저에서 즉시 사용할 수 있도록 **Streamlit Cloud**를 통해 배포되었습니다.

---

## ✨ 주요 기능

* **📝 텍스트 요약 (Summarization)**
  * 사용자가 입력한 긴 뉴스 기사나 텍스트를 `KoBART` 모델이 분석하여 핵심 내용 3줄로 요약합니다.
* **📡 외교부 소식 자동 수집 (Auto-Crawling)**
  * 외교부 공식 블로그(RSS)를 실시간으로 크롤링하여 최신 글 리스트를 가져옵니다.
* **🔗 원문 및 요약 동시 제공**
  * 크롤링된 뉴스의 제목, 원문 링크, 그리고 AI 요약본을 카드 형태로 직관적으로 제공합니다.

---

## 📂 프로젝트 구조

깃허브 리포지토리는 아래와 같이 구성되어 있습니다.

```bash
final/
├── app.py                # 메인 애플리케이션 (Streamlit 실행 파일)
├── requirements.txt      # 클라우드 배포를 위한 라이브러리 목록 (필수)
└── README.md             # 프로젝트 설명서

submissions/{학번}/assignment4/
├── data-analysis.ipynb        # (필수) Jupyter Notebook 또는 Colab 코드
├── data/                       # (필수) 데이터 파일
│   ├── data.csv (또는 .json)
│   └── (필요시) 추가 데이터 파일들
└── README.md  # (필수) 분석 결과 요약
