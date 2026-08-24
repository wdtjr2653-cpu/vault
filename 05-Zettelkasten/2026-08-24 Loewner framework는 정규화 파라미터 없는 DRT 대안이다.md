#zettel #drt-regularization #project/eis-to-drt

## 주장
Tikhonov 계열 DRT의 모든 불안정성은 결국 정규화 파라미터 λ 선택에서 나온다. **Loewner framework(LF)는 임피던스 데이터를 직접 보간하는 행렬 계산만으로 DRT를 추출하므로, λ라는 하이퍼파라미터 자체가 존재하지 않는다** — "λ를 더 잘 고르는 법"과 "λ가 필요 없는 방법"은 다른 축의 해법이다.

## 근거
- Loewner 방법의 Li-ion DRT 적용: Bayreuth 그룹, "Introducing the Loewner Method as a Data-Driven and Regularization-Free Approach for the DRT Analysis of Lithium-Ion Batteries" 및 *J. Power Sources* (2023, S0378775323009515).
- 잡음 내성 개선판 **Robust Loewner Framework(RLF)**: *J. Power Sources* (2025, S0378775325017458) — 튜닝·정규화 없이 잡음 하에서 기존 LF 대비 참 DRT 복원 우수, MATLAB GUI 코드 공개.
- 데이터 기반 EIS 분석 관점 정리: *iScience* (2025, S2589-0042(25)00247-0).

## 이 vault에서의 적용
[[2026-08-19 EIS_to_DRT 프로젝트 개요]]의 λ* 불안정(같은 셀 반복측정에서 550배 차이)은 L-curve를 GCV로 바꿔도 "λ를 고른다"는 구조가 남는다. LF는 그 구조 자체를 제거하는 대안이므로, GCV 교체 파일럿과 나란히 **같은 281개 데이터로 LF(또는 RLF) DRT를 뽑아 피크 위치·개수·면적의 재현성을 비교**해 볼 가치가 있다. 단 LF는 이산 극점(discrete poles)을 주므로 연속 분포 형태의 기존 시각화·피처와의 호환은 확인 필요.

## 관련
- [[2026-08-19 DRT 정규화 파라미터는 재표본추출과 교차검증으로도 검증한다]] — λ를 "잘 고르는" 축의 방법
- [[2026-08-19 DRT L-curve corner는 offset을 줘야 정확하다]] — 현행 λ 선택 방식
- [[2026-08-24 DRT 문헌 검증 및 최신 기법 조사]] — GCV/mGCV 권장 근거(Maradesa 2023) 포함 전체 조사
