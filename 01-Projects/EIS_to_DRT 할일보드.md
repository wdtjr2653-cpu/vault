---

kanban-plugin: board

---

## 할 일

- [ ] `train_classifier.py` 구현 시 `n_baseline_zscore()`를 **CV 매 fold 안에서** 호출할 것(전역 1회 호출 금지) + **Nested CV**(단순 CV는 n=282 소표본에서 낙관적 편향 — 임계값 튜닝과 평가를 분리) + 반복 stratified CV로 recall 신뢰구간 보고(fold당 N=8뿐이라 분산 큼) + **feature 목록에서 `lambda_star` 제외**(아래 최종결정 참고)
- [ ] **[별도 R&D 과제로 분리] λ 선택법을 GCV 계열로 교체** — 제약(non-negativity) 있는 최소자승 문제의 유효자유도 근사가 필요한 상당한 수치해석 작업. 참고: GCV/modified GCV/robust GCV 등 비교 문헌([DRTtools, ACS Electrochemistry 2025](https://pubs.acs.org/doi/10.1021/acselectrochem.5c00334)), Bayesian DRT(MCMC 불확실도 정량화)([Adaptive DRT Bayesian Mixtures, JPCC](https://pubs.acs.org/doi/10.1021/acs.jpcc.5c04766))
- [ ] 향후 신규 데이터 수집 시 그룹당 일부 셀에 2~3회 반복측정 프로토콜 반영 (실제 실행은 측정팀 협의 필요)
- [ ] SOH 예측용 신규 데이터 수집 실험 설계 (동일 셀에 EIS/DRT + 실측 용량검사 페어링) — 측정팀 협의 필요
- [ ] (참고, 후순위) L2(2차미분) Tikhonov 대신 entropy 기반 정규화 검토 — DRT 복원 오차 ~50% 감소 보고됨([ScienceDirect 2025](https://www.sciencedirect.com/science/article/abs/pii/S0378775325007463))

## 진행중


## 완료

- [x] **λ* 근본해결 시도 2건, 둘 다 실증에서 악화 확인 후 되돌림 → `lambda_star`를 feature에서 제외하는 것으로 최종 결정 (2026-08-20)**
  1. 그리드 확장(10→1000): 불량_A-12가 1.0x→215x로 악화(기존 그리드가 우연히 경계값에 "붙잡아뒀던" 것뿐이었음이 드러남)
  2. Hansen 스플라인 기반 곡률: 그리드 경계에서 인위적 스파이크, 최대 2700만x로 더 악화
  - `lam_grid_boundary_hit`(`DrtResult`)/`lambda_reliable`(summary.csv) 플래그는 유지 — 281개 전체 재실행 결과 16개(5.7%, N/불량 균등분포로 라벨 편향 없음) 그리드 경계 케이스만 부분적으로 걸러냄
  - `docs/specs/`·`docs/plans/` 설계문서에 최종 결정 반영 완료
- [x] **N-baseline z-score 피처 누수 수정 완료, 281개 전체 재실행으로 검증** — `features.py`: `add_n_baseline_feature()`(전체 데이터로 1회 계산, 누수) 제거 → `add_drt_tv_feature()`(raw `drt_tv`만 저장, 라벨 무관이라 안전) + `n_baseline_zscore(train_df, apply_df)`(fold-safe 원시함수, `train_classifier.py`가 CV 매 fold마다 새로 호출해야 함) 로 분리. 테스트 3개 작성·통과, 281개 샘플 전체 재실행 에러 0건 확인
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