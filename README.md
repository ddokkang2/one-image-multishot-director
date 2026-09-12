# One-Image Multi-Shot Director

Seedance 2.5용 독립 영상 연출 스킬입니다.

한 장의 기준 이미지와 간단한 콘셉트를 입력하면 다음 결과를 만듭니다.

1. 비주얼 앵커 요약
2. 15~30초 4단 멀티샷 타임라인
3. Seedance 2.5에 바로 붙여 넣는 영문 프롬프트 4종

이 스킬은 STORM, Notion, 특정 프로젝트와 연결되지 않은 독립 스킬입니다.

## 기본 30초 구성

- Shot 1: 0~5초 — 분위기와 공간 소개
- Shot 2: 5~12초 — 주요 감정·퍼포먼스
- Shot 3: 12~22초 — 얼굴 붕괴를 줄이는 매크로 인서트
- Shot 4: 22~30초 — 클라이맥스와 히어로 엔딩

## 설치

```bash
mkdir -p ~/.hermes/skills/one-image-multishot-director
cp SKILL.md ~/.hermes/skills/one-image-multishot-director/SKILL.md
```

자세한 사용법은 [MANUAL.md](MANUAL.md)를 참고하세요.
