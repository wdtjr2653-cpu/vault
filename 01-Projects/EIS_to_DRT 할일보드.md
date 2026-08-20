---

kanban-plugin: board

---

## 할 일

- [ ] `peak_regions()` 결과(Rohm/Rsei/Rct/W 구간별 저항)를 `summary.csv`에도 피처로 추가할지 검토 — 현재는 GUI 표시용으로만 연결됨, 분류기 feature로 편입하면 판별력 개선 가능성
- [ ] **측정팀과 협의 필요**: 저주파측(확산/Warburg 추정) 미해결 구간이 발생하는 26개 셀은 어떤 조건(불량 유형/온도/SOC 등)에서 나타나는지 원인 규명 — 통계(아래 완료 항목)는 "얼마나 자주·얼마나 크게"만 확인했고 "왜"는 미조사
- [ ] `train_classifier.py` 구현 시 `n_baseline_zscore()`를 **CV 매 fold 안에서** 호출할 것(전역 1회 호출 금지) + **Nested CV**(단순 CV는 n=282 소표본에서 낙관적 편향 — 임계값 튜닝과 평가를 분리) + 반복 stratified CV로 recall 신뢰구간 보고(fold당 N=8뿐이라 분산 큼) + **feature 목록에서 `lambda_star` 제외**(아래 최종결정 참고)
- [ ] **[별도 R&D 과제로 분리] λ 선택법을 GCV 계열로 교체** — 제약(non-negativity) 있는 최소자승 문제의 유효자유도 근사가 필요한 상당한 수치해석 작업. 참고: GCV/modified GCV/robust GCV 등 비교 문헌([DRTtools, ACS Electrochemistry 2025](https://pubs.acs.org/doi/10.1021/acselectrochem.5c00334)), Bayesian DRT(MCMC 불확실도 정량화)([Adaptive DRT Bayesian Mixtures, JPCC](https://pubs.acs.org/doi/10.1021/acs.jpcc.5c04766))
- [ ] 향후 신규 데이터 수집 시 그룹당 일부 셀에 2~3회 반복측정 프로토콜 반영 (실제 실행은 측정팀 협의 필요)
- [ ] SOH 예측용 신규 데이터 수집 실험 설계 (동일 셀에 EIS/DRT + 실측 용량검사 페어링) — 측정팀 협의 필요
- [ ] (참고, 후순위) L2(2차미분) Tikhonov 대신 entropy 기반 정규화 검토 — DRT 복원 오차 ~50% 감소 보고됨([ScienceDirect 2025](https://www.sciencedirect.com/science/article/abs/pii/S0378775325007463))

## 진행중


## 완료

- [x] **GUI 그래프 가독성 개선: 정사각(5:5) 비율 + 고정 축 범위 + 주파수 구간 색상 매핑 (2026-08-20)**
  - 사용자가 "등가회로 파라미터와 주파수별 저항성분 둘 다 표시할 필요가 있는지" 질의 → 확인 결과 R0=Rohm(R0), Rp=Σ(주파수별 성분)이 항상 같은 값(정의상 중복)이라 등가회로 파라미터 블록에서 R0/Rp를 빼고, 주파수별 성분 표에 "Σ(위 성분) = Rp와 일치" 검증 줄 하나로 합쳤음(정보 손실 없이 중복 제거)
  - Nyquist/DRT 서브플롯 가로세로비를 ~4:6→5:5로 조정(figsize 7.6×4.8→10.0×5.0, 창 너비도 1080→1360으로 확대)
  - 축을 파일마다 auto-scale하지 않고 전체 281개 실측 데이터 기준 고정값으로 통일: DRT τ축 1e-5~1e0(로그), γ축 0~0.7, Nyquist Z'·-Z''축 둘 다 0~0.65(equal aspect 유지하며 정사각 박스를 채우려면 x·y 스팬이 같아야 함을 확인 후 맞춤) — 파일 간 눈대중 비교가 가능해짐
  - `peak_regions()`가 반환하는 각 구간(Rohm 제외 Rsei/Rct/W/미해결)의 τ 경계를 Nyquist 측정점(f→τ=1/2πf 매핑)과 DRT 음영(axvspan)에 동일 색상으로 표시 — "이 반원이 이 저항 성분"이 시각적으로 대응되도록 함. 미해결(고/저주파측 절단) 라벨은 그래프에서는 "?"로 축약(전체 설명은 사이드 텍스트에만), 인접 라벨 겹침은 높이를 번갈아 배치해 해결
  - `batch_process.peak_regions()`에 `tau_lo_s`/`tau_hi_s`(구간 경계, 초) 필드 추가(이 매핑에 필요) — 기존 소비처(GUI만) 영향 없음, `process_one()`은 `peak_regions()` 미사용이라 무관
  - 실제 파일(N-1_1.csv, 불량 A-12_1.csv)로 렌더링 후 이미지로 육안 검증: 라벨 겹침 없음, 색상 대응 정상, Σ=Rp 정확히 일치 확인
- [x] **GUI(`gui_app.py`) 신규 제작 + Rohm/Rsei/Rct/W 구간별 저항 분해 기능 추가 (2026-08-20)**
  - ttkbootstrap 다크테마, 배경색 통일, 다중 CSV 동시 로드+콤보박스 전환, `.pyw` 콘솔없는 런처
  - **버그 발견·수정**: N-1_1.csv 예시로 "Nyquist엔 반원 2개인데 DRT엔 피크 1개만" 사용자가 지적 → GUI가 "감마값 상위 3개"로 피크를 뽑던 임시 로직이었고(하나의 넓은 피크 인접점만 3개 뽑힘), `batch_process.find_peaks()`(정상, 지역극대값 기반)는 원래 버그 없었음을 확인
  - **추가 발견**: N-1_1.csv는 τ 최대값(측정 최저주파수)까지 감마가 계속 상승만 하고 안 꺾임 = 확산/Warburg로 추정되는 3번째 공정이 측정 주파수 범위 밖에서 잘려있음. 기존 `peak_regions()` 1차 구현은 이 "잘린 꼬리"를 조용히 누락시켜 합계가 Rp의 32%밖에 안 됐음 → `x`(원시 저항질량, Rp=sum(x) 정의) 기반으로 재작성 + 미해결 구간을 별도 항목("미해결(저주파측 절단, 확산/Warburg 가능성)")으로 명시 포함 → 합계가 Rp와 정확히 일치하도록 수정 완료(실측 검증)
  - CSV 파서(`parse_eis_csv`)도 다른 컬럼명/레이아웃 자동감지 폴백 추가(`_parse_eis_csv_flexible`) — 표준형식 regression 없음, 합성 테스트로 검증
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