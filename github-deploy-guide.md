# yottol/news 배포 가이드 — 매일 08:00 KST 자동 업데이트

Nick 님 전용 배포 셋업. **처음 1회만** 15분 투자, 이후 매일 아침 자동 배포됩니다.

저장소: https://github.com/yottol/news

---

## 방법 A — 가장 쉬움 (GitHub 웹 UI로 매일 업로드, 2분)

매일 아침 Claude가 `2026-MM-DD.html`을 생성 → Nick 님이 드래그 드롭 한 번.

1. 브라우저에서 https://github.com/yottol/news 접속
2. `2026-04-21.html` 클릭 → 우상단 연필 ✏️ 아이콘
3. 새 HTML 내용 전체 붙여넣기 → 하단 `Commit changes` 버튼
   - 또는 파일 자체 업로드: `Add file` → `Upload files` → 드래그 드롭 → `Commit`
4. GitHub Pages가 이미 켜져있다면 1~2분 내 자동 배포

### GitHub Pages 활성화 (최초 1회)

1. 레포 → `Settings` → `Pages` (좌측 메뉴)
2. Source: `Deploy from a branch` → Branch: `main` / `(root)` → `Save`
3. 상단에 `Your site is live at https://yottol.github.io/news/` 표시됨

---

## 방법 B — Mac 터미널 자동 푸시 (한 번 셋업, 매일 10초)

### 최초 셋업

```bash
# 1. 레포를 맥에 클론 (홈 디렉토리 아무 곳이나)
cd ~
git clone https://github.com/yottol/news.git
cd news

# 2. GitHub 인증 (한 번만)
# 옵션 A: gh CLI 설치 후 로그인 (권장, 가장 간편)
brew install gh
gh auth login
# → GitHub.com → HTTPS → Yes → Login with a web browser → 프롬프트 대로 진행

# 옵션 B: Personal Access Token 발급 (gh CLI 없이)
# github.com/settings/tokens → Generate new token (classic) → repo 스코프 체크
# 생성된 토큰을 복사해서 macOS 키체인에 저장하거나, .netrc에 저장
```

### 매일 배포 (Cowork에서 Claude가 생성한 파일을 푸시)

```bash
cd ~/news
# Cowork가 만든 최신 HTML을 여기로 복사
cp "/Users/nick/Documents/AI 최신 뉴스 자동화/2026-04-21.html" .

# 커밋 & 푸시
git add 2026-04-21.html
git commit -m "$(date +%Y-%m-%d) daily AI brief"
git push
```

원하시면 위 세 줄을 `publish.sh`로 저장해서 매일 한 줄(`./publish.sh`)로 실행 가능합니다.

---

## 방법 C — GitHub Actions로 완전 자동화 (고급, 추천)

Cowork 스케줄러가 08:00 KST에 `2026-MM-DD.html`을 만들고 **레포로 바로 푸시**하도록 GitHub Actions + PAT를 걸어두면, Nick 님이 터미널을 안 열어도 됩니다. 필요하면 제가 `.github/workflows/` YAML을 짜드릴 수 있으니 말씀만 주세요.

---

## index.html 매일 자동 업데이트 포인트

`index.html`이 매일 새 날짜 HTML로 리다이렉트하도록 **한 줄만** 교체하면 됩니다.

```html
<meta http-equiv="refresh" content="0; url=2026-04-21.html">
```

매일 배포 시 위 줄의 날짜를 새 날짜로 바꿔 함께 커밋하면 루트(`https://yottol.github.io/news/`) 접속 시 항상 최신 브리핑으로 자동 이동합니다.

---

## 카톡 후크 메시지 (복사 & 붙여넣기용)

`repo/kakao-hook-YYYY-MM-DD.txt`에 매일 후크 메시지를 자동 생성하도록 스케줄 프롬프트에 포함시켰습니다. 내용 예시:

```
📡 4/21 (화) 해볼깡 일일 AI 트렌드
- 아마존, 앤트로픽에 추가 250억$ 투자
- 제미나이 인 크롬 한국 출시
- 마벨-구글 AI 칩 협력 보도
전체 보기 → https://yottol.github.io/news/
```

---

## 체크리스트

- [ ] 방법 A/B/C 중 하나 선택
- [ ] GitHub Pages 활성화 (`Settings → Pages → Source: main / root`)
- [ ] 매일 08:00 KST 스케줄 등록 완료 (Cowork에서 자동)
- [ ] 첫 수동 푸시로 배포 URL(`https://yottol.github.io/news/`) 확인
- [ ] (선택) Short.io 단축링크 생성
- [ ] (선택) 카톡방 공유 테스트
