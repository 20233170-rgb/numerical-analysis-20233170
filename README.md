# Water Potability Assessment & Golden Time Prediction
### (수질 데이터 분석을 통한 식수 적합성 판별 및 안전 섭취시간 예측)

분석 대상: 수질 데이터 (Organic Carbon, Turbidity 등) 및 세균 증식 모델
핵심 기술: K-Means Clustering, Logistic Regression, Malthusian Growth Model (ODE)
언어/환경: Python, Google Colab (Jupyter Notebook)

---


● 프로젝트 개요

이 프로젝트는 수질 데이터셋을 기반으로 머신러닝 기법을 활용하여 식수 적합성(Potability)을 판별하고, 나아가 수학적 모델링(미분방정식)을 결합하여 오염 수준에 따른 '섭취 가능 골든타임(Safe Consumption Window)'을 예측하는 것을 목표로 한다.

단순한 데이터 분류를 넘어, 실제 환경(정수기, 수돗물, 하천)을 가정한 시나리오 테스트를 통해 실생활에 적용 가능한 안전 가이드라인을 제시한다.


● 실행 방법

1) 라이브러리 설치
pip install pandas numpy matplotlib seaborn sklearn

2) 파일 준비
이 저장소(Repository)의 water_potability.csv와 .ipynb 파일을 다운로드
또는 Google Colab에서 해당 파일을 업로드하여 준비

3) 코드 실행
- 데이터 로드 및 전처리: 데이터 정제 및 특징 선택
- K-Means 수행: 안전/위험 군집 분류 및 시각화
- 시뮬레이션: 시간 경과에 따른 세균 증식 그래프 출력
- 결과 확인: 최종 시나리오별 Risk/Safe 판별 결과 출력

 


● 전처리 과정 요약

1. 결측치 제거: 데이터 신뢰성을 위해 결측값이 포함된 행 제거 (dropna)
2. 변수 선택: 세균 증식에 직접적인 영향을 미치는 핵심 변수 선정
   - Organic_carbon (유기탄소): 세균의 먹이 역할 (증식률 k 결정)
   - Turbidity (탁도): 세균의 서식처 역할 (초기 개체수 N0 결정)
3. 군집화 전처리: K-Means 알고리즘을 위한 데이터 스케일링 및 대표값(Centroid) 추출



● 분석 내용

1) 군집화 및 대표값 추출 (K-Means Clustering)
전체 데이터를 'Clean Group(안전)'과 'Dirty Group(위험)'으로 군집화
시뮬레이션에 사용할 각 그룹의 대표 환경 변수(Centroid) 산출
목적: 수천 개의 데이터를 개별 시뮬레이션하는 대신, 통계적 대표값을 통해 경향성 파악

2) 식수 적합성 판별 (Logistic Regression)
수질 변수(탄소, 탁도)가 식수 적합성(Potability)에 미치는 영향 분석
현재 수질 상태가 '식수'로 적합한지 판별하는 분류 모델 구축 및 정확도 평가

3) 골든타임 예측 시뮬레이션 (Mathematical Modeling)
Malthusian Growth Model (N(t) = N0 * e^(kt)) 적용
전처리된 데이터를 수식에 대입하여 시간 경과(t)에 따른 세균 증식량 예측
안전 기준치(예: 100 CFU)를 초과하는 시점 (안전시간) 산출

4) 시나리오 기반 위험도 평가
실제 환경을 가정한 3가지 케이스에 대한 모델 검증 수행
- Case 1: 정수기 물 (극한의 청정 상태)
- Case 2: 일반 수돗물 (환경부 수질 기준 근사치)
- Case 3: 오염된 하천수 (높은 유기물 및 탁도)






● 주요 결과 요약

군집 분석: 유기탄소와 탁도가 낮을수록 '식수 적합(Potability=1)' 비율이 높음 확인.
골든타임:
- 깨끗한 물(Clean Group)은 장시간 방치해도 세균 증식이 억제됨.
- 오염된 물(Dirty Group)은 초기 세균 수(N0)가 높고 증식 속도(k)가 빨라 단시간 내 위험 수치 도달.
결론: 탁도(Turbidity) 관리가 초기 세균 오염을 막는 핵심이며, 유기물(Organic Carbon) 관리는 증식 속도를 늦추는 데 중요함.



● 데이터 출처

출처: Kaggle Water Potability Dataset (Aditya Kadiwal via Kaggle)
데이터 종류: 유기탄소(Organic Carbon), 탁도(Turbidity), 식수 적합 여부(Potability) 등
파일명: water_potability.csv → (전처리 후) water_potability_processed.csv
