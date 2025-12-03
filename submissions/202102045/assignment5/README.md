## 1\. Project Overview

본 프로젝트는 **국제/정치 뉴스 및 공공기관 소식 자동 요약 봇**을 개발하기 위한 모델 학습, 평가, 그리고 실제 서비스 구현 과정을 담고 있습니다.

Assignment 4에서 수집한 뉴스 데이터로 모델을 학습(Fine-tuning)시키고, 이를 확장하여 **외교부 공식 블로그의 최신 소식을 RSS로 감지하여 자동으로 요약하는 파이프라인**까지 구축했습니다.

### 🎯 Key Goals

  - **Fine-tuning**: 한국어 뉴스 데이터셋을 활용해 KoBART 모델 최적화
  - **Automation**: RSS 피드를 활용한 실시간 뉴스 수집 및 요약 파이프라인 구축
  - **Evaluation**: ROUGE Metric을 활용한 정량적 성능 검증


## 2\. Directory Structure

제출된 프로젝트의 파일 구조는 다음과 같습니다.

```text
assignment5/
├── training.ipynb      # 모델 학습, 데이터 전처리, 가중치 저장
├── evaluation.ipynb    # Test Set 평가, ROUGE 점수 계산
├── inference.ipynb     # 모델 로드, 정적 예시 및 실시간 파이프라인 실행
└── README.md           # 프로젝트 문서 (현재 파일)
```


## 3\. Model Architecture

### 3.1 Model Selection

  - **Base Model**: `gogamza/kobart-summarization`
  - **Architecture**: **BART (Bidirectional and Auto-Regressive Transformers)**

### 3.2 Why KoBART?

BART는 Encoder(Bidirectional)와 Decoder(Auto-Regressive)를 결합한 Seq2Seq 구조를 가집니다. KoBART는 한국어 위키백과, 뉴스, 대화 등 대규모 코퍼스로 사전 학습되어 있어, **한국어 생성 요약(Abstractive Summarization)** 태스크에서 탁월한 성능을 보입니다.


## 4\. Training Details

### 4.1 Experimental Setup

  - **Dataset**: `daekeun-ml/naver-news-summarization-ko` (전처리 완료)
  - **Split Ratio**: Train(80%) / Val(10%) / Test(10%)
  - **Environment**: Google Colab (T4 GPU)
  - **Hyperparameters**:
      - `Epochs`: 3
      - `Batch Size`: 4
      - `Learning Rate`: 2e-5
      - `Max Input Length`: 512
      - `Optimizer`: AdamW

### 4.2 Training Process Analysis

**[Loss & Performance Curve]**

1.  **Training Loss (학습 손실)**

      - Epoch 1 (`0.46`) → Epoch 3 (`0.27`)로 지속적으로 가파르게 감소했습니다.
      - 이는 모델이 학습 데이터를 효과적으로 학습하고 있음을 나타냅니다.

2.  **Validation Loss (검증 손실)**

      - Epoch 2에서 `0.441`로 최저점을 찍은 후, Epoch 3에서 `0.445`로 아주 미세하게 상승했습니다.
      - 이는 모델이 Epoch 3 시점에서 일반화 성능의 정점에 도달했음을 시사하며, 더 이상의 학습은 과적합(Overfitting)을 유발할 수 있어 **3 Epoch에서 학습을 종료한 것이 적절한 판단**이었습니다.

3.  **Validation ROUGE Score**

      - ROUGE-L 점수가 약 34\~35점 대에서 안정적으로 유지되었습니다.


## 5\. Evaluation Results

Test Dataset(학습에 사용되지 않은 데이터)을 대상으로 **ROUGE Metric**을 사용하여 정량적 평가를 수행했습니다.

### 📊 Quantitative Results

| Metric | Score (%) | 의미 및 분석 |
| :--- | :---: | :--- |
| **ROUGE-1** | **58.49** | **매우 높음**. 기사의 핵심 키워드(Unigram)를 약 58% 이상 정확히 포착함. |
| **ROUGE-2** | **37.71** | **우수함**. 두 단어 연속 표현(Bigram)의 일치도가 높아 문맥 흐름이 자연스러움. |
| **ROUGE-L** | **55.39** | **매우 높음**. 문장 구조적 유사도가 55%를 상회하여, 사람의 요약과 구조가 흡사함. |

> **종합 평가**: 일반적인 요약 모델의 ROUGE-1 점수가 40\~50점 대인 것을 감안할 때, **58.49점**은 매우 우수한 성능입니다.


## 6\. Inference Pipeline & Analysis

본 과제에서는 단순 예시 출력을 넘어, 실제 활용 가능한 **자동화 파이프라인**을 구현했습니다.

### 6.1 Feature: 외교부 소식 자동 요약기

  - **기능**: 외교부 공식 블로그의 RSS 피드를 모니터링하여 '외교부 소식' 카테고리의 최신 글을 자동으로 감지합니다.
  - **프로세스**:
    1.  `rss.blog.naver.com` 파싱으로 최신 게시글 URL 자동 추출
    2.  Iframe 구조를 해제하여 본문 크롤링
    3.  학습된 KoBART 모델로 3줄 요약 생성

### 6.2 Qualitative Analysis (정성 평가)

실제 외교부 블로그 글 요약 결과(`inference.ipynb` 실행 결과)를 분석한 내용입니다.

1.  **높은 핵심 정보 포착 능력**

      - 게시글 [1], [2] 등에서 '박윤주 1차관', '앨리슨 후커', '마시모 아파로' 등 주요 인물의 이름과 직책, 날짜, 회의 목적을 정확하게 요약했습니다.

2.  **문장 잘림 현상 (Truncation Issue)**

      - **현상**: 게시글 [3]의 마지막 부분("...한국과 쿠바의 선")과 같이 문장이 맺어지지 않고 끊기는 현상이 발생했습니다.
      - **원인**: `max_length` 제한(150토큰)에 도달하여 생성이 강제 종료되었습니다.


## 7\. Model Weights Access

평가 기준에 따라 학습된 모델 가중치는 Google Drive에 저장되어 있으며, 아래 링크를 통해 다운로드할 수 있습니다.
(`inference.ipynb` 실행 시 해당 경로에서 자동으로 로드됩니다.)

  - **저장 위치**: Google Drive (`/content/drive/MyDrive/NLP_Assignment5/final_model`)
  - **공개 다운로드 링크**: [[Google Drive Model Download Link](https://drive.google.com/drive/folders/1mVQn_VeouAAeB2Ft5xM3PjTFnHCHnWCf?usp=drive_link)](https://drive.google.com/drive/folders/1mVQn_VeouAAeB2Ft5xM3PjTFnHCHnWCf?usp=drive_link)


## 8\. Analysis & Limitations

### 8.1 Limitations (한계점 및 대책)

1.  **문장 반복 현상 (Repetition Issue)**

      - 일부 결과에서 동일한 문장이 반복되는 현상이 관찰되었습니다.
      - **Solution**: Inference 단계에서 `no_repeat_ngram_size=3` 파라미터를 적용하여 해결했습니다.

2.  **문장 끊김 현상 (Truncation Issue)**

      - **현상**: 긴 본문을 요약할 때, 설정된 최대 길이(`max_length`) 제한으로 인해 문장이 완벽하게 맺어지지 않고 중간에 끊기는 현상이 일부 관찰되었습니다.
      - **Solution**:
          - **파라미터 조정**: 추론 시 `max_length`를 150 이상(예: 200\~256)으로 확장하여 충분한 생성 길이를 보장합니다.
          - **페널티 부여**: `length_penalty` 파라미터를 조정하여 모델이 문장을 끝맺을 때까지 생성을 지속하도록 유도합니다.
          - **후처리**: 문장이 완성되지 않은 경우(마침표로 끝나지 않음), 마지막 문장만 제거하는 후처리 로직을 도입합니다.

3.  **데이터 도메인 편향 (Data Bias)**

      - 학습 데이터의 대부분이 경제/사회 뉴스에 집중되어 있어, 프로젝트 목표인 '정치/국제' 분야의 전문 용어 처리가 부족할 수 있습니다.

### 8.2 Future Work (향후 계획)

  - **도메인 적응**: BBC News 등 정치 도메인 데이터를 추가 확보하여 재학습(Re-training)을 시도할 계획입니다.
  - **파라미터 튜닝**: Beam Search의 Beam Size를 조절하여 생성 다양성을 확보할 예정입니다.


## 9\. Inference Examples (Real-time Results)

`inference.ipynb`를 실행하여 **실시간으로 외교부 블로그 최신 글 5건을 자동 수집 및 요약**한 결과입니다.

### [게시글 1] 외교부 1차관, 美 국무부 정무차관 면담(12.2.)

> **AI 요약**: 박윤주 외교부 제1차관은 12.2.(화) 오후 미국 국무부에서 앨리슨 후커 국무부 정무차관을 면담하고 한일 정상회담 후속조치, ▴대북 공조 및 ▴지역·글로벌 정세 관련 의견을 교환하고 한미 관계 관련 오랜 전문성을 바탕으로 분야별 실무협의체 가동 등을 통해 구체적이고 가시적인 성과가 도출될 수 있도록 노력해달라고 당부했다. 박 차관은 두 차례의 성공적 한미 정상회담 개최로 한미 관계가 그 어느 때보다 굳건하게 발전하고 있다고 평가하고, 후속 조치의 충실한 이행을 챙겨 나가겠다고 했다.

### [게시글 2] 제14차 한-국제원자력기구(IAEA) 고위급 정책협의회 개최

> **AI 요약**: 12.2.(화) 오전 외교부에서 마시모 아파로 국제원자력기구(IAEA) 안전조치 사무차장과 제14차 한-IAEA 고위급 정책협의회(ROK-IAEA High-level Policy Consultation)를 개최하여 IAEA의 핵심 업무 영역인 안전조치 관련 주요 현안을 점검하고, 양측 간 협력 확대 방안을 모색하기 위해 2013년부터 매년 개최되어 온 고위급 소통 채널이다.

### [게시글 3] 한국과 쿠바의 선율이 한 무대에, 한-쿠바 친선음악회 개최

> **AI 요약**: 외교부는 12월 2일(화) 푸르지오 아트홀에서 오후 2시와 7시 30분, 두 차례에 걸쳐 ‘한국-쿠바 친선음악회: 아바나에서 서울까지 음악여행’을 개최했는데, 2024년 2월 한국과 쿠바 간 외교관계 수립 이후 양국은 활발한 문화·청년 교류를 이어오고 있으며, 수교 1주년을 맞아 아프로쿠반 재즈의 신예 청년 뮤지션인 ‘아브레우 형제 트리오’와 라틴 퍼커션의 거장 ‘야롤디 아브레우스’를 초청하여 한국의 25현 가야금 연주자 서정민과 함께 한국과 쿠바의 선

### [게시글 4] 민관합동 「수출‧수주 외교지원단」 출범 및 제1차 회의 개최

> **AI 요약**: 12.2.(화) 오후 우리 기업의 수출‧수주 지원을 위한 민간 합동 협의체인 「수출∙수주 외교지원단」을 출범하고, 김진아 제2차관(단장) 주재로 산업통상부, 중소벤처기업부, 국토교통부 등 정부부처와 민간경제단체가 참여하는 제1차 회의를 개최하였으며 특히 수출 기업을 대표하는 여러 경제단체와의 직접적인 소통을 통해 수출현장과 연계된 기업체감적인 수출‧ 수주 지원 방안을 적극 모색해 나갈 예정이다.

### [게시글 5] 마약예방 수칙과 함께하는 안전한 해외여행

> **AI 요약**: 식품의약품안전처, 외교부, 관세청은 최근 우리 국민의 해외 마약범죄 연루 위험이 나날이 증가하고 있어, 겨울방학 등 휴가시즌인 12월 1일부터 해외여행객을 대상으로 해외 마약 노출 위험성·주의사항 등을 홍보하며, 단 한 번만 연루되어도 법적 처벌로 이어지며, 마약을 직접 사용할 경우에는 심각한 신체적·정신적 부작용도 함께 겪을 수 있기 때문에 사전에 올바른 정보를 알고 예방하는 것이 무엇보다 중요하다고 전했다.
