# Portfolio Builder — Progress

## 완료

### 빌더 (localhost:8765)
- [x] Python 서버 + builder.html
- [x] 프로젝트 목록 / 에디터 / 프리뷰 3패널 레이아웃
- [x] 이미지 자동선별, 드래그 순서변경, 캡션, 컬럼 설정
- [x] Desktop / Mobile 프리뷰 토글 (iframe)
- [x] Export HTML (로컬 다운로드)

### Generate
- [x] Claude CLI 연동 (`claude --allowedTools Read`)
- [x] 볼트 `voice.md` 룰북 삽입
- [x] 볼트 `inbox/내가 쓴 글.md` 톤 예시 삽입
- [x] 볼트 `portfolio/` 승인 글 우선 예시
- [x] Race condition 수정 (프로젝트 전환 중 결과 덮어쓰기 방지)

### 배포
- [x] GitHub 레포 (`heeyechoi/portfolio`) 연결
- [x] Vercel 자동 배포 (main push → 자동 반영)
- [x] 도메인 연결: `ordk.kr` → Vercel (DNS A 레코드 설정)
- [x] ⬆ Publish 버튼 (빌더에서 클릭 → GitHub push → Vercel 배포)

### 이미지 최적화
- [x] 원본 840MB → `_web/` 최적화본 ~12MB
- [x] JPEG 82% / 1920px max / ASCII 번호 파일명 (001.jpg, 002.jpg…)
- [x] `_map.json`으로 원본↔웹파일명 매핑
- [x] `*.gitignore`로 원본 이미지 제외, `_web/`만 커밋

### 사이트 디자인 / 프론트엔드 (2026-08-10)
- [x] 홈: 룰러(15px) + 드래그 가이드라인(블랙, 새로고침 시 리셋) + 드래그 가능한 텍스트 블록
- [x] 홈: 진입 시 타이핑 애니메이션 (제목 → 소개문 → 메뉴 순 페이드인)
- [x] 홈: 마우스 트레일 이미지 (프로젝트 대표 이미지 랜덤, 좌측 메뉴존 제외, 클릭 시 유지)
- [x] 홈 텍스트 블록을 단일 플로우 컨테이너로 재구성 (좁은 화면에서 메뉴 겹침 해결)
- [x] 드로어: 하단에서 올라오는 패널 (데스크톱 85vh, 반투명 흰색 65% + 배경 블러)
- [x] 드로어 상세: 정보 / 이미지(중앙) / 설명(우측) 3분할, 라이트박스 갤러리(호버 화살표, × 닫기)
- [x] 반응형 브레이크포인트 정리 — 모바일 ≤768 / 태블릿 769–1350 / 데스크톱 1351+
- [x] 태블릿·모바일: 카테고리 상단 가로줄 + 프로젝트 리스트 접이식 토글
- [x] 태블릿·모바일: 닫기 버튼을 카테고리 줄 우측에 배치 + 수직 중앙정렬, 여백 균등화
- [x] 태블릿·모바일: 정보/설명/카테고리를 홈 텍스트 좌측선에 정렬 (태블릿 35px / 모바일 30px)
- [x] 모바일: 드로어 풀스크린(100dvh), 이미지 1장 스와이프 캐러셀, 갤러리뷰 비활성화
- [x] 데스크톱↔모바일 리사이즈 시 이미지 사라짐 버그 수정 (`mob-active` 복구 핸들러)
- [x] 커스텀 SVG 화살표 커서 (index.html 인라인 data URI, 트레일 이미지 위에서도 유지)
- [x] 메뉴 e-mail 클릭 → mailto 대신 주소 클립보드 복사 ("copied!" 피드백)

### 사이트 개편 (2026-08-10) — Works 2단계 구조 + 인터랙션 (커밋 3f5af18, 21fce38)
> 위 "드로어 상세 3분할 + 라이트박스" 는 이 개편으로 **대체됨**.

**홈**
- [x] 드로어/아카이브/어바웃 배경 블러 16 → **4px**
- [x] 메뉴 링크 `display:inline-block` (글자 폭만 클릭), About·Instagram 아래 줄바꿈 추가
- [x] 홈 텍스트: 타이핑 완료 후 **단어별 span 분리 → 개별 드래그**, 메뉴 링크는 드래그 시 클릭 무시
- [x] **About 탭** 추가: `#about` 오버레이(Archive와 동일 패널), `/* ABOUT:START/END */ var ABOUT` 마커를 publish가 빌더 `localStorage['about-text']`로 채움 + 빌더 About 편집 모달
- [x] 커스텀 커서 3종: 기본 **45° 회전 + 5% 축소**, 이미지 위 좌/우 방향 반전 커서(`--cur-left/right`)

**Works 드로어 — 이미지 중심 목차 → 상세 (2단계)**
- [x] 좌측 카테고리 필터 + 프로젝트 리스트 유지. `#dr-main` 이 `mode-list`/`mode-detail` 토글
- [x] **목차(리스트)**: 프로젝트별 카드 = 전 이미지 가로 스트립 + 메타(제목/Type·Date/Client/Categories)
  - [x] **전광판 마퀴**(transform 기반 연속 스크롤 110px/s, 호버 정지)
  - [x] **클릭앤드래그 스크럽** / 그냥 클릭 → 상세 이동 (4px 임계로 구분)
  - [x] 세로 스크롤 시 현재 프로젝트를 **좌측 리스트에서 굵게**(scroll-spy)
  - [x] 커서 = **채워진 점**(`#dragdot`, `mix-blend-mode:difference` 반전), 드래그 중 **빨강**
- [x] **상세**: 상단 스와이프 스트립(좌/우 반 클릭으로 페이징, easeOutBack, **끝에서 멈춤·루프X**, 340ms)
  - [x] 위치기반 좌/우 화살표 커서
  - [x] 메타 헤더(제목·Type/Date | Client | Category | Field | **Credit**) — Credit 이름 링크(빌더 role/name/url 편집)
  - [x] 작품설명을 **Client 열과 좌측정렬**(grid `2 / 5`, 우측 끝 4·5열 사이)
  - [x] 설명 아래 **이미지 순서대로 세로 갤러리** + 호버 캡션, 맨 아래 **`↑ (top)`** 좌측정렬 버튼
- [x] `(Close)` / `(Back to List)` 버튼 = 오버레이 + **`mix-blend-mode:difference`** 반전
- [x] 프로젝트 개요 회색 글씨 → 전부 검정
- [x] 라이트박스(이미지 클릭 팝업) **삭제**
- [x] 전역 **`word-break:keep-all`** — 단어 안 잘리고 어절 단위 줄바꿈
- [x] 행간: 국문 1.5 / 영문 1.3 / 메타값 1.5

> ⚠️ **배포 방식**: index.html은 손으로 편집한 뒤 `git commit && git push origin main`으로 직접 배포한다.
> 빌더의 ⬆ Publish(`/api/publish`)는 index.html을 빌더 데이터로 **재생성**하므로 수동 디자인 편집을 덮어쓴다 — 디자인 변경 후에는 사용하지 말 것.

### voice.md (2026-08-11)
- [x] 신규 inbox 파일 `inbox/피하고 싶은 글.md` 추가 (금지사항 근거 전용, "내가 쓴 글"/"좋아하는 글"과 같은 성격의 3번째 원본)
- [x] 금지사항에 "~를(을) 짰다" 추가 (이유 없이 행위만 서술하는 어투, 규칙 1 위반 근거)

### 빌더 기능 확장 (2026-08-11)

**3탭 왼쪽 패널**
- [x] Projects / Archive / About 3탭으로 재구성
- [x] Archive 탭: 이미지 업로드(`POST /api/upload-archive`), 이미지별 title·caption·date 편집, 미리보기 실시간 반영
- [x] About 탭: 6열 그리드 인라인 편집 (기존 모달 폐기), 입력 즉시 미리보기 반영
- [x] Archive·About 탭 선택 시 미리보기가 해당 오버레이 자동 오픈

**Projects 에디터**
- [x] 눈 아이콘 토글로 프로젝트 노출/숨김 (숨김 시 Publish에서 제외)
- [x] 이미지별 눈 아이콘 토글 (숨김 이미지 Publish에서 제외)
- [x] 날짜 필드 → 연도·월 드롭다운 (연도 최신순, 월 1~12)
- [x] 프로젝트 목록 날짜 최신순 자동 정렬
- [x] Gallery Grid: 프로젝트별 1·2·3·4단 그리드 + 여백 유무 설정
- [x] 이미지별 컬럼 span 설정 (1~galleryColumns)
- [x] 크레딧 표시: `Role.` + 줄바꿈 + 이름 형식
- [x] Archive 에디터: 작업연도·월 드롭다운 추가

**이미지 에디터**
- [x] ratio·zoom·posX·posY·bg 설정값을 사이트(strip·gallery)에 실제 반영 (`applyImgCell` / `applyImgTransform`)
- [x] 에디터(`rt-box`)와 사이트 모두 `object-fit:contain`으로 통일 → 동일하게 보임

**빌더 레이아웃**
- [x] 왼쪽 패널 200px → 260px, 에디터 비율 확대, 프리뷰 비율 축소

**사이트 기능**
- [x] 홈 마우스 트레일 이미지 — PROJECTS + ARCHIVE 데이터에서 자동 생성 (하드코딩 제거)
- [x] Archive 각 셀: 이미지 → 제목 → 날짜 → 캡션 순 표시
- [x] About 패널: 6열 그리드 (데스크톱 6열 / 태블릿 3열 / 모바일 2열)
- [x] 갤러리 이미지 호버 불투명 효과 제거

**버그 수정**
- [x] `_web/Hotel GOYO branding` 대소문자 불일치(Vercel 이미지 404) → `git mv`로 수정
- [x] 서버 재시작 없이는 server.py 변경사항 미반영 — 재시작 후 Archive·About Publish 정상화

**코드 정리 (2026-08-11, Codex 리뷰 후)**
- [x] `index.html`: 라이트박스 전체 삭제(~80줄), `projectImgList` fallback 단순화
- [x] `builder.html`: `selectImg`·`optCanvas`·`_invalidateArchiveCache`·`renderPrev` 래퍼 등 데드코드 제거, 중복 fetch·slug 로직 통합
- [x] `server.py`: `IMG_EXT` 모듈 상수화, `_json`/`json` 중복 메서드 통합

### 배포 방식 변경 (2026-08-11)
> ⚠️ **현재 배포 방식**: index.html 수동 편집 후 `git commit && git push origin main` 직접 배포.
> 빌더 Publish는 PROJECTS·ARCHIVE·ABOUT 마커 블록만 교체하므로 나머지 수동 편집은 보존됨.
> **server.py 변경 후에는 서버를 반드시 재시작**해야 변경사항이 반영됨.

### 상세/모바일 다듬기 (2026-08-10~11) — (커밋 378f6dc, 50f53b2)

**상세페이지 개요(`.dv-head`)**
- [x] 그리드 **5열 → 6열**: 1열 제목/Type·Date, **2열 빈 칸(`.dv-spacer`)**, 3열 Client, 4열 Category, 5열 Field, 6열 Credit
- [x] 작품설명(`.dv-desc`)도 한 칸 밀어 **Client(3열)와 좌측정렬**, 우측 끝 5·6열 경계(`grid-column: 3 / 6`)
- [x] 태블릿·모바일은 `.dv-spacer` 숨김 → 기존 3열/2열 유지
- [x] 개요 캡션 라벨↔값 갭 제거(`.dv-k` margin-bottom 0), 제목↔Client 간격(`.dv-title-col` padding-right 32px)
- [x] 개요 값(`.dv-v`) 행간 **1.5 → 1.3**
- [x] 목차 카드 간격 64→**40px**(데스크톱) / 40→**30px**(모바일)
- [x] 상세 하단(`↑ (top)` 아래) 여백 절반: 데스크톱 48→**24px**, 태블릿 40→**20px**

**태블릿·모바일 상세 = 세로 나열**
- [x] 상단 **가로 스와이프 스트립(`.dv-strip`) 숨김** → 설명 아래 세로 갤러리(`.dv-gallery`)만 노출
- [x] 모바일: 호버 불가라 갤러리 캡션을 이미지 **아래 정적 텍스트**로 표시(`.dv-gallery .dr-cap` static)
- [x] 모바일 드로어 좌우 패딩 균등(우측 20→**30px**), 모바일 홈 `#dt2` 너비 `100vw-60px`(좌우 30px 균등)

**데스크톱·태블릿 상세 풀스크린 확장**
- [x] 설명 아래 갤러리가 뷰로 들어오면 드로어 `height` → **100dvh**(`.expanded`), 위로 스크롤하면 85vh 복귀
  - `#dr-detail` scroll에서 `.dv-gallery` 위치로 토글(확장 0.5·복귀 0.7 히스테리시스), `isMobile()` 가드, 목록 복귀·닫기·프로젝트 전환 시 해제

**홈**
- [x] 메뉴 링크 호버색 회색(`#888`) → **빨강(`#ff2a2a`)**

---

### 빌더 이미지 파트 전면 재설계 (2026-08-11~13)

**이미지탭 / 텍스트탭 구조**
- [x] 이미지 섹션을 탭 블록 기반으로 재설계 — 이미지탭·텍스트탭 각각 추가 가능
- [x] 탭 블록 드래그로 순서 이동
- [x] 이미지 드래그 → 탭 내 순서 변경 + 탭 간 이동
- [x] 탭별 여백(gap) 토글 / 보이기 토글 (눈 아이콘 → 슬라이드 토글 통일)
- [x] 탭 이름 클릭해서 편집 (contenteditable)
- [x] 이미지 캡션 편집 → 이미지 클릭 팝업(조정 모달) 안으로 이동
- [x] 텍스트탭 — 국문 / 영문 2열 편집

**이미지 레이아웃 시스템 (6컬럼 CSS Grid)**
- [x] 이미지별 size: 1(100%) / 2(50%) / 3(33%) 설정
- [x] 이미지별 align: L(좌) / C(가운데) / R(우) 설정 (size 2→L·R, size 3→L·C·R)
- [x] 탭당 최대 3장 제한 (+버튼 3장 시 자동 숨김)
- [x] 같은 row에 나란히 배치 가능 (size2-L + size2-R → 한 줄에 50+50)
- [x] hover 시 size/align 컨트롤 버튼 오버레이 표시
- [x] 이미지 셀 4:3 비율 고정, `object-fit:contain` — 세로사진 양쪽 여백 처리
- [x] site(`index.html` loadProject 갤러리) 도 동일한 6컬럼 grid + size/align 반영

**카테고리 / 필드 커스텀 추가**
- [x] 각 섹션 하단 pill 스타일 입력창 — Enter로 새 항목 추가, localStorage 저장
- [x] 추가된 항목 모든 프로젝트에서 공통 사용

**줄바꿈 웹 반영**
- [x] `index.html` `.dv-body-ko` / `.dv-tagline` / `.dv-body-en` → `white-space:pre-line`
- [x] Export HTML에도 동일 적용

**빌더 에디터 UI 통일**
- [x] Korean / English 섹션 → **Description** 2컬럼으로 통합 (스크롤 감소)
- [x] × 삭제 버튼 `.btn-x` 단일 클래스로 통일 (크레딧·탭 삭제 동일 스타일)
- [x] 이미지탭추가 / 텍스트탭추가 → `.btn-sm` 클래스로 inline override 제거
- [x] 카테고리·필드 추가 input pill 스타일로 통일
- [x] ig-ctrl-btn hover 상태 추가
- [x] `.sab` (+ 크레딧 추가) dashed border로 "추가" 액션 시각화
- [x] 프로젝트 리스트 패널 260px → **320px** 확대, 에디터 비율 축소

---

### 버그 수정 · UI 통일 (2026-08-15)

**Archive**
- [x] GIF가 퍼블리시에서 빠지던 버그 수정 (`IMG_EXT`에 `.gif` 누락 → `PUB_EXT` 분리, GIF는 sips 변환 없이 그대로 복사)
- [x] Archive 메뉴 설명문 추가 (사진 그리드 위, works 카테고리와 동일 스타일)
- [x] 캡션 입력 시 사진 크기가 달라지던 버그 수정 (`.ar-cell`에 `min-width:0` 누락 → grid 컬럼이 캡션 길이에 밀림)
- [x] 텍스트 순서 확정: 타이틀 → 캡션 → 날짜, 행간 1.3
- [x] "AI-assisted work" 체크박스 추가 (체크 시 날짜 옆 회색 12px 표시)
- [x] 날짜 최신순 정렬 (`_archive_date_key`, 날짜 없는 항목은 맨 뒤)
- [x] Archive / Works 새로고침 아이콘 추가 (폴더에 파일 추가 후 리로드 없이 목록 갱신) — 아이콘만 정중앙 기준 회전하도록 별도 span으로 분리
- [x] `.tif`/`.tiff` 지원 추가 (퍼블리시 시 JPEG로 자동 변환)
- [x] `_map.json`에서 사라진 원본 파일 매핑이 안 지워져 같은 이미지가 두 번 뜨던 버그 수정 (퍼블리시마다 stale entry 정리)
- [x] 모바일에서 설명문이 `white-space:nowrap`으로 잘리던 것 → 모바일만 `normal`로 줄바꿈 허용

**닫기 버튼 (Archive / About)**
- [x] Works 드로어와 동일하게 통일: `(Close)` 텍스트, 흰색 + `mix-blend-mode:difference`, hover 시 opacity
- [x] 스크롤하면 버튼이 같이 밀리던 버그 수정 (패널 자체의 `transform`이 자식 `position:fixed` 요소의 containing block이 되는데, 그 패널에 스크롤도 같이 걸려있어서 버튼이 콘텐츠와 함께 움직였음 → 스크롤을 내부 wrapper(`#archive-scroll`/`#about-scroll`)로 분리)

**빌더**
- [x] 이미지 크기(1/2/3) · 정렬 설정이 저장 안 되던 버그 수정 (`persistImg`가 자동숨김(15장 초과)된 이미지를 못 찾아 조용히 실패 → 전체 이미지 목록 기준으로 찾도록 수정)
- [x] `start.command`가 예전 경로(`/Users/heeye/portfolio`)를 가리켜 항상 실행 실패하던 버그 수정 → `/Users/heeye/projects/portfolio`로 정정

**신규 프로젝트 퍼블리시 버그**
- [x] 새 프로젝트 첫 퍼블리시 시 이미지 경로가 원본 파일명으로 나가서 실제 최적화 파일명(`001.jpg`…)과 안 맞아 전부 깨지던 버그 수정 — 퍼블리시 시점에 서버가 방금 만든 `_map.json` 기준으로 `PROJECTS[].images[].file`을 다시 맞춰 쓰도록 수정 (Archive와 동일한 방식)
- [x] 폴더명에 악센트 문자(예: "ēndline")가 있으면 이미지가 전부 404나던 버그 수정 — macOS는 파일명을 분해형(NFD)으로 저장하는데 Vercel은 결합형(NFC)으로 매칭 → 퍼블리시 시 폴더명을 NFC로 정규화하도록 수정

---

## 진행 중 / 남은 작업

### 🟡 콘텐츠
- [ ] dotdotdot 프로젝트 — Generate 실행
- [ ] endline 프로젝트 — Generate 실행
- [ ] 볼트 `portfolio/` 폴더에 승인 글 추가 (최종 확정 텍스트)
- [ ] Archive 이미지 title·caption·date 입력 후 Publish

### 🟢 선택
- [ ] ordk.kr 도메인·SSL 최종 확인

---

## 파일 구조

```
/Users/heeye/projects/portfolio/   ← 빌더 루트 (서버 실행 위치)
  builder.html                     ← 빌더 UI (3탭: Projects / Archive / About)
  server.py                        ← Python HTTP 서버 (변경 후 재시작 필요)
  start.command                    ← 더블클릭으로 서버 실행
  index.html                       ← 포트폴리오 사이트 (PROJECTS·ARCHIVE·ABOUT 마커 블록)
  _web/                            ← 최적화 이미지 (001.jpg…)
  Archive/                         ← Archive 원본 이미지
  works/                           ← 프로젝트별 원본 이미지

/Users/heeye/projects/portfolio wiki/   ← Obsidian 볼트
  voice.md                              ← 문체 룰북 (Generate 프롬프트 삽입)
  inbox/내가 쓴 글.md                   ← 톤 예시
  inbox/피하고 싶은 글.md               ← 금지사항 근거
  portfolio/                            ← 승인 글 (우선 예시로 사용)
```

## 사이트

| | URL |
|---|---|
| 빌더 | http://localhost:8765 |
| 실제 사이트 | https://ordk.kr |
| GitHub | https://github.com/heeyechoi/portfolio |

> ⚠️ Vercel 배포 URL(`*.vercel.app`)은 배포마다 바뀌고 SSO로 막혀있어 직접 접속 불가 — 항상 `ordk.kr`로 확인할 것.
> (예전에 적혀있던 `portfolio-five-pearl-89.vercel.app`은 이 프로젝트와 무관한 다른 사이트였음 — 2026-08-15 확인)
