#zettel #drt-regularization #project/eis-to-drt

## 주장
Tikhonov 정규화로 DRT를 계산할 때, L-curve의 **global corner(최대곡률점)를 그대로 λ로 쓰면 안 된다.** Global corner에서 더 큰 λ(더 매끄러운) 방향으로 offset을 준 지점을 써야 고주파 영역의 노이즈가 사라진다.

## 근거
Paul, Chi, Wu & Wu, *Scientific Reports* 11, 12624 (2021). ⚠️ 기존에 "Effat & Wang, 12967"로 오기재되어 있던 것을 2026-08-24 Google Scholar 검증으로 정정(Effat는 Ciucci 그룹의 다른 논문 저자 — 혼동 주의). 단일 RC 시뮬레이션·이중 RC·슈퍼커패시터·Li-ion 반쪽전지 4개 사례 전부에서 global corner는 노이즈 섞인 DRT를 냈고, offset을 준 지점만 "noise free" DRT를 냈다고 보고.

**단, offset을 얼마나 줄지는 논문에 공식이 없다.** 4개 사례의 offset λ값이 9×10⁻³(단일 RC) ~ 0.0659(Li-ion)까지 제각각 — 전부 그래프를 육안으로 보고 정한 값. 즉 "적당히 더 매끄러운 쪽으로" 이상의 정량적 규칙은 없다.

## 이 vault에서의 적용
[[2026-08-19 EIS_to_DRT 프로젝트 개요]]의 `drt_core.py`에 `_l_curve_corner(..., offset_steps=3)`로 구현. 3을 고른 근거는 이 논문 자체가 실제 Li-ion 반쪽전지(α-LiFeO₂/Li 코인셀)에서 분해해낸 피크 개수(3개: 표면피막/전하이동/미확정 저주파 공정)에 잔피크 수가 가장 가깝게 수렴하는 지점이었기 때문 — 공식이 없으니 "이 데이터셋에서 물리적으로 그럴듯한 지점"을 기준으로 삼음.

## 관련
- [[2026-08-19 곡선 이상치는 자기 그룹이 아니라 건강 기준 대비로 판정해야 한다]] — 같은 프로젝트에서 나온, "공식 없는 판정 기준은 상대적 비교보다 절대적/외부 기준이 안전하다"는 자매 교훈
- 원문: `이정석\01-Projects\EIS_to_DRT\논문\Computation of distribution of relaxation times by Tikhonov regularization for Li ion batteries usage of L curve method.pdf`
