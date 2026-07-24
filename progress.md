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
