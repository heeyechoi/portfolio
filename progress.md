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

> ⚠️ **배포 방식**: index.html은 손으로 편집한 뒤 `git commit && git push origin main`으로 직접 배포한다.
> 빌더의 ⬆ Publish(`/api/publish`)는 index.html을 빌더 데이터로 **재생성**하므로 수동 디자인 편집을 덮어쓴다 — 디자인 변경 후에는 사용하지 말 것.

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
  portfolio/                    ← 승인 글 (우선 예시로 사용)
```

## 사이트

| | URL |
|---|---|
| 빌더 | http://localhost:8765 |
| Vercel | https://portfolio-five-pearl-89.vercel.app |
| 도메인 | https://ordk.kr (DNS 전파 후) |
| GitHub | https://github.com/heeyechoi/portfolio |
