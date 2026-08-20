#area/notebook

원본: 손글씨 노트북 사진 필사 정리, `이정석/02-Areas/Notebook/`
(IMG_8495와 IMG_8510은 동일 페이지 중복 촬영이라고 문서에 적혀있으나, 실제 폴더에는 IMG_8498~8512(15장)만 존재 — IMG_8495~8497은 확인 안 됨. 원본 필사이므로 일부 약어·수치는 실제 노트 대조 권장)

## 원본 사진
- [IMG_8498.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8498.jpeg>)
- [IMG_8499.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8499.jpeg>)
- [IMG_8500.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8500.jpeg>)
- [IMG_8501.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8501.jpeg>)
- [IMG_8502.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8502.jpeg>)
- [IMG_8503.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8503.jpeg>)
- [IMG_8504.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8504.jpeg>)
- [IMG_8505.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8505.jpeg>)
- [IMG_8506.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8506.jpeg>)
- [IMG_8507.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8507.jpeg>)
- [IMG_8508.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8508.jpeg>)
- [IMG_8509.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8509.jpeg>)
- [IMG_8510.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8510.jpeg>)
- [IMG_8511.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8511.jpeg>)
- [IMG_8512.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8512.jpeg>)
- [IMG_8543.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8543.jpeg>)
- [IMG_8547.jpeg](<C:/Users/MONA/OneDrive - 모나일렉트릭 주식회사/바탕 화면/이정석/02-Areas/Notebook/IMG_8547.jpeg>)

## 1. AI·데이터사이언스 스터디 (Titanic 데이터셋 실습)

### 8/4 — Pandas 기초
- pd.DataFrame ≒ Matrix 구조: column = key, row = 데이터(레코드)
- .loc(라벨 기반) / .iloc(인덱스 기반) 슬라이싱, NaN 처리
- Feature engineering 개념 정리, dropna(), column 선택/삭제
- Decision Tree 개념: split → leaf → prediction, 트리가 깊을수록 정교한 예측

### 8/5 — 모델링 기초 & Overfitting/Underfitting
- Feature Selection: describe()로 컬럼 통계 확인 후 X(feature), y(target) 분리
- scikit-learn 워크플로: Define → Fit → Predict → Evaluate
- Model Validation: MAE = mean(|actual − predicted|)
- In-sample score의 함정 → validation data 분리 필요(train_test_split)
- Overfitting/Underfitting: Tree Depth 증가 시 Training error는 감소, Validation error는 U자형
- RandomForestRegressor(random_state=1) → fit → predict → mean_absolute_error
- Feature 전처리: dtype 확인, 상관관계 분석(Pearson's r / Theil's U / Correlation Ratio), Data Imputation, Label Encoding

### 8/6 — Feature 정리 & Pipeline
- OrdinalEncoder(categories=[[...]]) 사용, numpy array vs list 차이 주의
- 전처리 파이프라인: Pipeline(steps=[('num_imputer', SimpleImputer), ...])
- ColumnTransformer로 수치형/범주형 분리 전처리 → OrdinalEncoder/OneHotEncoder + StandardScaler
- 모델 후보: Linear Regression, Decision Tree Regressor, Random Forest Regressor, Gradient Boosting Regressor
- cross_val_score(pipeline, X, y, cv=5, scoring='neg_mean_absolute_error')

### 8/10 — Titanic 데이터셋 실전 적용
- 개별 승객 케이스 확인 (Ellen Needs 생존, Kelly Mr. James 사망 등)
- 도메인 배경: 1912.4.15 타이타닉 침몰, 승객·승무원 약 2,224명 중 생존율 약 32%
- 컬럼: Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked
- Workflow 7단계: ①분류 → ②상관관계 분석 → ③데이터 변환 → ④결측치 보완 → ⑤이상치 제거/차팅 → ⑥새 feature 생성(예: SibSp+Parch=FamilySize) → ⑦분류/차팅
- 실전 아이디어: Age 결측치 보완, Fare→1인당 환산, Cabin 첫 글자만 추출

### 8/20 — 앙상블 모델(RandomForest/XGBoost) & 모델 평가
- 모델 평가지표: MAE = mean_absolute_error
- 트리 계열 앙상블 개념 다이어그램: ①단일 의사결정 트리 → ②랜덤포레스트(배깅) → ③XGBoost(그래디언트 부스팅)
- SPARSE_output=True/False 옵션 메모: False일 때 np.ndarray로 처리 필요 — Pandas DataFrame이 그대로 처리되지 않는 이유 정리
- Out of sample(OOS): test data / valid data 구분
- Feature/Target 설계: Feature 약 22개(feature_x1~x22), Target은 분류 라벨(예: A/B/C-D 등) — Feature와 Target을 명확히 정리하는 것이 중요하다는 메모
- RNN, CNN, CLF 등 모델 유형 비교 언급 (필체 일부 판독 불확실, 원본 대조 권장)

## 2. 회사 업무·기획 미팅 노트

### 8/6 — SoH(Apple/HYC) 측정 데이터 논의
- SoH 관련(Apple, HYC 겸용) 측정 주파수 범위 논의
- High freq / Low freq 특성 차이, Watch 기기 측정 대역 1Hz~1,200Hz
- 10~100Hz 구간 특이 패턴 검토
- KETI·JIAT 관련 일정 조율(8/12~14 등)

### 8/7 — KETI 미팅 (BaaS/SDV)
- BaaS(Battery as a Service) 개념 정리
- SDV(Software Defined Vehicle): HW-SW 분리 아키텍처, SoC 논의
- BMS·EIS 관련 사업화 방향 논의
- 8/17 후속 일정, 오프라인 미팅 예정

### 8/9 — KETI 방문 후속
- 자동차 SW 생태계, HW/SW 분리(SDV) 트렌드, 전자 시스템 SoC 동향
- 시장 리서치: KB증권 리포트 등 인용, ESS/모바일向 시장 규모
- Tesla 등 경쟁사 사례, NVIDIA·MCT 관련 메모

### 8/11 — AI Sprint 미팅
- RER 관련 팀 미팅, JIAT 관련 데모 일정(8/13)
- HYC report 작성: Test condition, Applied Voltage(AC amplitude, mV) 정리
- 측정 시간, 다중 측정(wide) 조건 비교
- Gamry vs 자체 장비 비교, std range(min-max) 편차 확인

### 8/12 (오전) — 진행 상황 점검
- 전체 진행률 점검, ZP RFQ 진행 상황(HW/SW 항목 구분)
- 통합 업무 범위 정리, 필요 사항(needs) 2가지 식별
- 스타트업 시장 접근 전략, A안/B안/C안 비교
- 마일스톤: ~8/22, ~9/15, ~12/24
- BBD·WIPS(특허 검색 시스템) 메모, 11/24 관련 일정

### 8/13 — 국가 R&D 과제·특허 조사 (AD SP)
- IPC vs CPC 특허분류 비교 조사
- TUV Nord Korea 등 인증기관 파악, ESS 시장 특허 동향
- 국내 특허 출원 트렌드(2016·2019·2024년 등 시계열)
- CLI 기반 데이터 조사, HTC Room / RTC 기간 도출식, CEO 미팅 관련

### 8/20 — BMS 데이터 기반 AI 서비스 기획
- BMS 데이터 처리 output을 json 포맷으로 정리, BMS data는 DB로 관리
- Cloud 서버 후보 비교: AWS, Google, Naver
- 공용 platform 형태로 데이터를 확보·활용하는 방향 논의
- 채용/일정 관련 요일별 To-do 메모(8/24, 8/26, IRIS 등 언급) — 필체 판독이 어려운 부분이 많아 원본 사진 대조 필요

## 3. Si 음극재·DRT 연구 노트

### 8/14 — Si Anode 특성 & DRT 적용
- Si anode 이론 용량: 약 3,000~4,000 mAh/g (흑연 대비 매우 높음)
- Volume Expansion 문제: 충방전 시 300~400% 부피 팽창
- Li ↔ LiₓSi ↔ Graphite intercalation 비교 구조
- V.E. → Pulverization → SEI 파괴·재형성 반복 → 비가역 용량 손실 증가
- SiOₓ 반응식: SiO₂ + 4Li⁺ + 4e⁻ → 2Li₂O + Si (비가역적 리튬 소모)
- 해결책: Artificial SEI 형성, Pre-lithiation, Si 나노입자화(150nm 이하)로 pulverization 억제

**EIS → Si anode 적용 메모 (주파수 대역별 저항 성분 분리, DRT 활용)**
- 10k~100kHz: Ohmic Resistance (전해질/집전체 저항)
- 1k~10kHz: SEI Resistance
- 1~1kHz: Charge Transfer Resistance
- <1Hz: Warburg (확산 저항)
- DRT로 각 성분을 broadening 형태로 분리·시각화, 반응이 다양해질수록 피크 확장

**HYC meeting 메모**
- 인가 전압 진폭: 10mV(RMS) 기준, 측정시간 약 10min
- Chamber 온도 조건: 25 ± 0.5°C
- Low frequency 대역 노이즈 이슈 확인, full version 측정 1건 예정 → [[2026-08-18 HYC FUEIS 검증 프로젝트 개요]]와 연관

### 8/18 — Si 코인셀 EIS 불량검출 실험 메모
1. 셀 테스트는 SOC 35%에서 먼저 진행하고 100%에서 재검사함 — 이유는 35%에서 불량이 제대로 검출되지 않기 때문. 다만 두 번 테스트하면 비용 부담이 커서, **SOC 100%로 가지 않고 formation 없이 35%에서 EIS로 모든 불량을 검출**하는 게 목표
2. Hi-pot(내전압 검사) 기법에 대한 설명을 자세히 조사해올 것
3. 음극이 Silicon 100%라 volume expansion이 무조건 발생함 — 이 부피팽창으로 인한 short를 감지하려는 목적 (1번과 연관). **Silicon 100% 음극의 부피팽창 비율 조사 필요**
4. SEI층까지만 확인하면 부피팽창으로 인한 쇼트 감지가 될 것으로 보임 — 시간 단축을 위해 **어느 Hz까지 측정하면 되는지, 인덕턴스는 어디까지 찍어야 하는지**, 이를 통해 불량을 추론할 수 있는지 확인 필요

