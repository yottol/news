# 해볼깡 일일 AI 트렌드

매일 아침 08:00 KST, B2B 실무자 관점으로 AI 서비스·모델·규제 업데이트를 정리합니다.

## 폴더 구조

```
repo/
├── index.html           # 루트 진입 → 최신 브리핑으로 리다이렉트
├── YYYY-MM-DD.html      # 날짜별 일일 브리핑 (아카이브)
└── og/                  # OG 이미지 저장소 (선택)
```

## 배포

- 호스팅: Cloudflare Pages (GitHub 저장소 연결, push 시 자동 배포)
- 단축 링크: Short.io
- 애널리틱스: Cloudflare Web Analytics (쿠키 없음)

## 운영 플로우

1. 08:00 스케줄러가 `YYYY-MM-DD.html` 자동 생성
2. `index.html`의 refresh 태그를 새 날짜로 업데이트
3. GitHub push → Cloudflare Pages 자동 배포
4. Short.io 단축링크 갱신
5. 카톡 오픈채팅방에 후크 메시지 + 단축링크 발송

## 라이선스

© 해볼깡 (Nick). 모든 원문 기사는 출처 링크의 저작권을 따릅니다.
