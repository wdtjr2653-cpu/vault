---

kanban-plugin: board

---

## 할 일

- [ ] 2단계(AI 진단) 설계로 전환 검토
- [ ] 데이터 수집 설계 시 반복측정 권장사항 반영 여부 논의 ([[2026-08-19 DRT 정규화 파라미터는 재표본추출과 교차검증으로도 검증한다]])
- [ ] visualize_groups.py 최종 group plot 육안 리뷰

## 진행중


## 완료

- [x] EIS→DRT 변환 파이프라인 기본 구현 (`drt_core.py`)
- [x] L-curve offset 적용 ([[2026-08-19 DRT L-curve corner는 offset을 줘야 정확하다]])
- [x] KK 저주파 절단 적용
- [x] 글리치 자동감지·제거 구현 ([[2026-08-19 단일 포인트 글리치는 곡선 range 대비 절대비율로 잡아야 오탐이 없다]])
- [x] N-baseline spike 판정 로직 적용 ([[2026-08-19 곡선 이상치는 자기 그룹이 아니라 건강 기준 대비로 판정해야 한다]])


%% kanban:settings
```
{"kanban-plugin":"board"}
```
%%