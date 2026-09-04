#project/cycler-ui-ux #status/진행중

## 개요
- 모나일렉트릭 사이클러(충방전기) UI/UX 개발 프로젝트 (2026-09-04 시작)
- Workspace: `이정석\01-Projects\Cycler_UI_UX\` (OneDrive 바탕화면)
- Claude Code 세션 저장소: `C:\Users\MONA\orca\projects\Cycler UI_UX` (git, 현재 빈 저장소)

## 자료 수급 (2026-09-04)
메일 "Cycler src, ref" (monagcp@gmail.com, cycler 연결 PC에서 수집) 첨부를 workspace에 정리:
- `src\cycler-main-master` — STM32 메인보드 펌웨어 (CubeMX, EWARM)
- `src\cycler_channel_fw` — STM32 채널보드 펌웨어 (Ver 0.11~0.13)
- `src\cycler_gui_win` — Windows GUI 소스 (C#, BMSManager.sln, .NET + EntityFramework + SQLite)
- `ref\MONA` — 소스를 빌드·설치한 BatteryCycler.exe 실행본 (설치 폴더 통째)
- `ref\BTS_UI확인용` — Neware BTS 8.0 참고용 설치 패키지 (설치 7z + 매뉴얼 + 한국어UI 설정, README_설치안내.txt 참고)
- `captures\` — BTS Client/BTSDA/설정화면 캡처 PNG 5장
- ⚠️ 메일 첨부 `cycler_capture.zip`(709B)은 내용이 빈 zip — 재전송 필요할 수 있음

## 목표
- `src`의 소스로 `ref\MONA`의 BatteryCycler.exe와 동일한 구동이 가능하게 빌드/재현
- UI/UX 개선 (BTS 8.0 UI를 벤치마크 참고)

## 빌드 재현 성공 (2026-09-04)
- `src\cycler_gui_win\BMSManager.sln` (.NET Framework 4.8 WinForms, 프로젝트 3개: BMSManager→BatteryCycler.exe / LogDataAnalyzer / IPAddressControlLib)
- VS2022 MSBuild, Release|Any CPU 첫 빌드에 성공 — NuGet은 Newtonsoft.Json 13.0.1 하나뿐, packages 폴더 동봉이라 restore 불필요
- 빌드본·ref 실행본 모두 버전 1.0.0.6 동일. 실행 확인: 다크 테마 메인화면(채널 그리드 + 장비 그리드 + 검사설정/시작/중지) 정상 표시
- `BatteryCycler.json`은 최초 실행 시 자동 생성(포트 6010, 기본 비번 1234를 DPAPI 암호화). **ref의 json은 사이클러 PC(사용자 60V400A)의 DPAPI로 암호화돼 있어 이 PC에서 못 씀** — 복사 금지
- 시험 시나리오는 `ref\MONA\Config\*.json`(평문 JSON)을 빌드 출력의 `Config\`로 복사해서 사용
- ref exe(582KB)가 빌드본(360KB)보다 큰 것은 빌드 구성 차이로 추정 (버전 동일)

## 다음 단계
- 실장비 구동 화면 자료 확보 후 UI/UX 개선 설계 (Claude design에서 시안 작업 예정)

## 작업 로그
```dataview
LIST
FROM #project/cycler-ui-ux
WHERE file.name != this.file.name AND !contains(file.folder, "05-Zettelkasten")
SORT file.name DESC
```
