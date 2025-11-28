# Assignment 5: Reddit Sentiment Analysis Model Technical Report

## 1. 모델 개요 및 설계 사양 (Model Overview and Design Specifications)

* **설계 목적 (Objective):** 본 연구는 Reddit 주식 관련 게시글의 비정형 텍스트 데이터를 정량적으로 분석하여, 시장 참여자의 투자 심리(Bullish/Bearish)를 이진 분류(Binary Classification)하는 알고리즘 모델을 구현하는 것을 목적으로 한다.

* **아키텍처 구성 (Architecture Configuration):**

  * **특성 추출 (Feature Extraction):** TF-IDF Vectorizer (최대 특성 수: 1,000개로 제한)

  * **분류기 (Classifier):** SGDClassifier (로그 손실 `log_loss` 기반의 로지스틱 회귀 적용)

* **선정 근거 (Rationale for Selection):**

  * 본 아키텍처는 텍스트 데이터가 내재적으로 지닌 고차원 희소성(High-dimensional Sparsity) 문제를 효과적으로 제어하고 연산 효율성을 극대화하기 위해 채택되었다.

  * `partial_fit` 메서드를 통한 온라인 학습(Online Learning)의 연산 가속성 및 계산 효율성이 확보된다.

  * 복잡한 블랙박스 모델 대비 결과에 대한 명확한 해석 가능성(Explainability)을 제공한다.

## 2. 데이터셋 분할 프로토콜 (Dataset Partitioning Protocol)

전체 원천 데이터는 모델 학습 및 평가의 객관성을 담보하기 위하여 층화 추출법(Stratified Sampling)이 적용된 다음 비율로 엄격하게 분할되었다. (난수 시드값: 42)

| 분할 (Split) | 비율 (Ratio) | 기능적 역할 (Functional Role) | 
| ----- | ----- | ----- | 
| **Train** | 80% | 모델 가중치 최적화 및 학습 (Backpropagation 수행) | 
| **Validation** | 10% | 에포크(Epoch)별 성능 모니터링 및 과적합(Overfitting) 방지 | 
| **Test** | 10% | 최종 모델 성능의 객관적 검증 (학습 과정에서 완전히 배제됨) | 

## 3. 학습 방법론 및 프로세스 (Training Methodology and Process)

* **에포크 (Epochs):** 총 30회 반복 수행이 결정되었다.

* **손실 함수 (Loss Function):** 로그 손실 (Log Loss)이 적용되었다.

* **모니터링 (Monitoring):** 매 에포크 종료 시마다 훈련 손실(Training Loss)과 검증 정확도(Validation Accuracy)가 추적되어 학습 곡선의 수렴 여부를 시각화되었다. 상세한 학습 추이 데이터는 `training.ipynb` 문서를 통해 검토 가능하다.

## 4. 정량적 평가 결과 (Quantitative Evaluation Metrics)

다음은 테스트 데이터셋(Test Set)에 대한 최종 성능 평가 수치이다. (`evaluation.ipynb` 실행 결과 기준)

| 평가지표 (Metric) | 점수 (Score) | 비고 (Remarks) | 
| ----- | ----- | ----- | 
| **정확도 (Accuracy)** | 100% | 전체 예측 데이터 중 정답 데이터의 비율 | 
| **F1-Score** | 1.0 | 정밀도(Precision)와 재현율(Recall)의 조화 평균 | 

*(주: 상기 수치는 예시 데이터에 기반한 결과이며, 실제 데이터 학습 시 변동 가능성이 있음을 명시한다.)*

## 5. 아티팩트 보존 및 재현성 (Artifact Persistence and Reproducibility)

학습이 완료된 모델의 가중치 및 벡터라이저 객체는 프로젝트의 재현성 확보를 위하여 `models/` 디렉터리 내에 영구적으로 보존 및 관리된다.

* **파일 저장 경로 (File Locations):**

  * `models/sentiment_model.joblib`: 학습된 분류기 모델 객체

  * `models/tfidf_vectorizer.joblib`: 학습된 특성 추출기 객체

  * `models/test_set.csv`: 성능 평가를 위한 테스트 데이터셋

* **실행 및 재현 (Execution Procedure):**
  `inference.ipynb` 스크립트가 실행될 경우, 상기 모델 아티팩트가 자동으로 로드되며, 별도의 재학습 절차 없이도 즉각적인 추론(Inference) 테스트 수행이 가능하도록 구성되었다.

제출자: 

$$
본인의 이름/학번
$$
