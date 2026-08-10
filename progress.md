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

## 진행 중 / 남은 작업

### 🔴 긴급
- [ ] `_web/Hotel GOYO/`, `_web/dotdotdot/` 구 PNG 파일 삭제
- [ ] 빌더에서 Publish 눌러 index.html ASCII 경로로 재생성 후 push
- [ ] Vercel에서 사진 정상 로드 확인

### 🟡 콘텐츠
- [ ] dotdotdot 프로젝트 — Generate 실행 (현재 Hotel GOYO 데이터 오염)
- [ ] endline 프로젝트 — Generate 실행
- [ ] 볼트 `portfolio/` 폴더에 승인 글 추가 (최종 확정 텍스트)

### 🟢 선택
- [ ] ordk.kr DNS 전파 완료 확인 (최대 24h)
- [ ] Vercel 커스텀 도메인 SSL 인증 확인

---

## 파일 구조

```
/Users/heeye/portfolio/         ← 빌더 루트 (서버 실행 위치)
  builder.html                  ← 빌더 UI
  server.py                     ← Python HTTP 서버
  start.command                 ← 더블클릭으로 실행
  index.html                    ← 생성된 포트폴리오 사이트
  fonts/                        ← SuisseIntl (Vercel 서빙용)
  _web/                         ← 최적화 이미지 (001.jpg…)
  Hotel GOYO/                   ← 원본 이미지
  dotdotdot/
  endline 25ss Visual Directing/

/Users/heeye/portfolio wiki/    ← Obsidian 볼트
  voice.md                      ← 문체 룰북 (Generate 프롬프트 삽입)
  inbox/내가 쓴 글.md            ← 톤 예시
  inbox/피하고 싶은 글.md         ← 금지사항 근거
  portfolio/                    ← 승인 글 (우선 예시로 사용)
```

## 사이트

| | URL |
|---|---|
| 빌더 | http://localhost:8765 |
| Vercel | https://portfolio-five-pearl-89.vercel.app |
| 도메인 | https://ordk.kr (DNS 전파 후) |
| GitHub | https://github.com/heeyechoi/portfolio |
