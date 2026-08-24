#zettel #drt-concept #project/eis-to-drt

## 주장
DRT는 병렬 RC(단일 시간상수) 공정의 합이라는 가정 위에 서 있다. 확산(Warburg)은 이 가정에 맞지 않아서, **유한길이 Warburg를 DRT로 전개하면 단일 피크가 아니라 무한 R//C 급수의 감쇠 피크 열로 퍼진다**(Boukamp의 해석해). 그래서 확산 구간에서 "피크 개수를 세고 면적을 귀속"하는 해석은 원리적으로 애매하다. 확산은 **DDT(distribution of diffusion times) 같은 확산 전용 분포나, CNLS의 명시적 Warburg 요소로 다루는 것이 맞다.**

## 근거
- Boukamp: FLW(finite-length Warburg)의 DRT 해석해 유도 — 무한 R//C 분해 구조 확인.
- DDT 프레임: *Phys. Rev. Lett.* 120, 116001 (2018) — 랜덤 FLW/Gerischer 병렬 배열의 분포 반전, Si 나노와이어 Li-ion 전극 사례 포함.
- LIB 확산 현상의 DRT 거동 조사: *Electrochim. Acta* (2022, S0013468622013317).

## 이 vault에서의 적용
[[2026-08-19 EIS_to_DRT 프로젝트 개요]]의 현행 설계 두 가지가 이 원리와 부합함을 확인: (1) `peak_regions()`가 저주파 꼬리를 피크로 세지 않고 "미해결(확산 가능성)"로 별도 표기하는 것, (2) CNLS(`ecm_fit.py`)가 확산을 DRT 피크가 아닌 명시적 semi-infinite Warburg 요소로 두는 것. 반대로 **DRT 피크 개수 기반 피처(피크1~3)에 확산 구간이 섞이면 노이즈가 된다** — 분류기 피처 설계 시 확산 구간(τ>10⁻¹s)의 피크는 개수 피처에서 제외하거나 별도 취급할 것.

## 관련
- [[2026-08-24 저주파 DRT 정보는 EIS 대신 전류 펄스 완화에서도 얻을 수 있다]] — 같은 저주파/확산 구간의 측정 축 해법
- [[2026-08-19 EIS로 겹친 전극반응은 DRT로 시계열 분리한다]] — DRT의 기본 가정(병렬 RC 합)을 명시하는 보완
