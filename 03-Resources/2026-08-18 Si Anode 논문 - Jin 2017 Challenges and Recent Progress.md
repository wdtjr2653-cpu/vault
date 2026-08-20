#source/paper #domain/si-anode

## 서지정보
- 제목: Challenges and Recent Progress in the Development of Si Anodes for Lithium-Ion Battery
- 저자: Yan Jin, B. Zhu, Z. Lu, Nian Liu, J. Zhu
- 저널: Advanced Energy Materials, 7, 1700715, 2017
- DOI: [10.1002/aenm.201700715](https://advanced.onlinelibrary.wiley.com/doi/full/10.1002/aenm.201700715)
- 원문 PDF 확보됨 (`이정석/03-Resources/Study/Battery_Study/`)

## 왜 Si인가
Si 원자 1개가 Li 4개와 결합 가능 → 흑연(6개 탄소당 Li 1개) 대비 이론 용량이 약 10배 (Li₄.₄Si 기준 4212 mAh/g vs 흑연 372 mAh/g). 지구상 두 번째로 풍부한 원소라 저비용 잠재력도 큼.

## 근본 문제 두 가지
1. **Pulverization(미세분쇄)**: 리튬화 시 부피팽창 최대 ~420% (Si→Li₄.₄Si) → 큰 응력으로 균열·분쇄 → 전기적 접촉 소실, 용량 저하
2. **SEI 불안정**: 부피변화로 SEI막이 계속 깨짐 → 매번 새로 두껍게 재형성 → 쿨롱효율 저하, 저항 증가

## Pulverization 해결책 — ⭐ 8/18 노트의 "150nm" 수치 출처
- **나노와이어**: 응력을 잘 흡수, 10사이클 후 용량 유지율 75%
- **나노입자 크기 임계값 발견 (Huang et al.)**: 개별 Si 나노입자를 in-situ TEM으로 관찰한 결과, **입자 지름이 약 150nm 미만이면 리튬화 시 균열이 전혀 발생하지 않음**. 150nm 이상이면 표면 균열 후 파괴. → **이게 8/18 실험 메모에 적힌 "Si 나노입자화(150nm 이하)로 pulverization 억제"의 원출처**
- 요크-쉘(yolk-shell) 구조, 다공성 네트워크도 부피변화를 흡수해 pulverization 방지

## SEI 안정화 해결책
- 이중벽 Si-SiOx 나노튜브: 6000사이클에서 평균 쿨롱효율 99.938%, 용량 88% 유지
- 요크-쉘(Si나노입자 코어 + 비정질 탄소 쉘): 탄소쉘과 입자 사이 빈 공간이 부피팽창을 흡수, 바깥쪽 SEI는 안 깨짐 (인공 SEI 개념)
- 그래핀 층으로도 SEI 안정화 가능

## 나노소재를 쓸 때 새로 생기는 3가지 문제 (실용화의 진짜 장벽)
1. **초기 쿨롱효율(Initial CE) 저하**: 표면적이 커서 SEI 형성에 리튬을 많이 소모 — Si 첫 사이클 CE는 보통 65~85%로 흑연(90~94%)보다 낮음
   - 해결책: 이차구조 설계(포메그래닛 구조 등 전해질 차단층으로 CE 90%대까지 개선), **프리리티에이션**(전기화학적 방식/SLMP 분말/LixSi 나노입자 — 90~100%대 CE 달성), 전해질 첨가제(FEC가 가장 유망, 첫 SEI층을 먼저 형성해 EC/DEC 분해 억제)
2. **면적당 용량(Areal capacity) 저하**: 나노입자는 tap density가 낮아 입자간 공간 커짐 → 같은 무게라도 부피가 커지고 전자 이동경로가 길어짐
   - 해결책: 마이크론 크기 이차구조(tap density ↑), 전도성 바인더(자가치유 폴리머 등, 파쇄돼도 스스로 재접합)
3. **소재 단가**: 복잡한 합성공정·고순도 원료 → 저등급 실리콘(금속급/페로실리콘, $0.6~1/kg)이나 천연 원료(왕겨, 모래)로 대체 가능성 제시

## 결론
지난 10년간 나노구조 설계로 pulverization·SEI 문제는 상당히 해결됐지만, **어느 구조도 초기CE·면적용량·단가 세 가지를 동시에 만족시키지 못함** — 앞으로는 이 셋을 함께 푸는 복합구조가 필요하다는 게 이 리뷰의 결론. 또한 대부분의 연구가 half-cell(Li metal 상대전극) 기준이라, 실제 상용화 평가엔 full-cell 성능 검증이 필수라고 지적.

## 관련
- [[Notebook 필사 정리]] — 8/14, 8/18 메모의 Si anode·volume expansion·pulverization·SEI·150nm 나노입자화 내용이 이 논문 원문과 정확히 대응
- [[2026-08-18 Si Anode 논문 - Pendashteh 2024 Nanotextile 100pct Si Anodes]] — 이 논문이 소개한 "나노와이어는 pulverization에 강하다"(Chan 2008 인용)는 원리를 2024년에 100% Si 나노와이어 텍스타일 구조로 확장 구현한 후속 연구
