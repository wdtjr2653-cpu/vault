---

kanban-plugin: board

---

## 할 일

- [ ] **[신규, 우선] N-baseline z-score 피처 누수 수정** — `features.py`의 `add_n_baseline_feature()`가 train/test 분할 전에 전체 N=40 샘플로 median/scale을 한 번만 계산해 `summary.csv`에 고정함. CV의 각 fold test-N 샘플이 자기 자신의 baseline 계산에 포함되는 leakage. Fold별로 train-N만으로 재계산하도록 수정 필요 (2026-08-20 코드 리뷰에서 발견)
- [ ] **[신규, 우선] `lambda_star`를 분류기 feature로 쓰기 전에 재현성 문제부터 해결** — 아래 "λ* 550배 차이" 항목 미해결 상태로 설계 스펙 feature 목록에 이미 포함됨. 노이즈 큰 피처가 그대로 들어가면 분류기가 우연한 상관을 학습할 위험 (2026-08-20 코드 리뷰)
- [ ] λ 탐색 그리드 상한 확장 (불량_A-32가 현재 그리드 최댓값 10에 걸림)
- [ ] 불량_Test-H15 반복측정 간 λ* 550배 차이 원인 조사 (L-curve+offset 재현성 문제) — 참고: GCV/modified GCV/robust GCV 등 L-curve 대안 비교 문헌([DRTtools, ACS Electrochemistry 2025](https://pubs.acs.org/doi/10.1021/acselectrochem.5c00334)), Bayesian DRT(MCMC 불확실도 정량화)로 근본 원인 진단 가능([Adaptive DRT Bayesian Mixtures, JPCC](https://pubs.acs.org/doi/10.1021/acs.jpcc.5c04766))
- [ ] 향후 신규 데이터 수집 시 그룹당 일부 셀에 2~3회 반복측정 프로토콜 반영 (실제 실행은 측정팀 협의 필요)
- [ ] SOH 예측용 신규 데이터 수집 실험 설계 (동일 셀에 EIS/DRT + 실측 용량검사 페어링) — 측정팀 협의 필요
- [ ] `train_classifier.py` 구현: RandomForest 이진분류 + **Nested CV**(단순 CV는 n=282 소표본에서 낙관적 편향 — 임계값 튜닝과 평가를 분리) + 반복 stratified CV로 recall 신뢰구간 보고(fold당 N=8뿐이라 분산 큼)
- [ ] (참고, 후순위) L2(2차미분) Tikhonov 대신 entropy 기반 정규화 검토 — DRT 복원 오차 ~50% 감소 보고됨([ScienceDirect 2025](https://www.sciencedirect.com/science/article/abs/pii/S0378775325007463))

## 진행중


## 완료

- [x] `features.py` 구현: `summary.csv` 재생성 + N-baseline 이상치 거리 피처 추가 (git branch `feat/2단계-ai-진단-이진분류기`, 아직 main 미병합 — vault에 반영 안 되어 있었음, 2026-08-20 확인)

- [x] EIS→DRT 변환 파이프라인 기본 구현 (`drt_core.py`)
- [x] L-curve offset 적용 ([[2026-08-19 DRT L-curve corner는 offset을 줘야 정확하다]])
- [x] KK 저주파 절단 적용
- [x] 글리치 자동감지·제거 구현 ([[2026-08-19 단일 포인트 글리치는 곡선 range 대비 절대비율로 잡아야 오탐이 없다]])
- [x] N-baseline spike 판정 로직 적용 ([[2026-08-19 곡선 이상치는 자기 그룹이 아니라 건강 기준 대비로 판정해야 한다]])
- [x] visualize_groups.py 최종 group plot 육안 리뷰 — N/불량_B/불량_F 이미지 확인, 수치와 일치 검증
- [x] Schlüter 재표본추출+분산검정 구현 및 실제 3쌍 파일럿 검증 ([[2026-08-19 DRT 정규화 파라미터는 재표본추출과 교차검증으로도 검증한다]])
- [x] 2단계 AI 진단 브레인스토밍 — SOH 데이터 소스 부재 확인, 양품/불량 이진분류기 설계 확정·스펙 작성 ([[2026-08-19 SOH 예측 모델은 EIS 측정과 실측 SOH가 페어링된 데이터가 필요하다]])


%% kanban:settings
```
{"kanban-plugin":"board"}
```
%%