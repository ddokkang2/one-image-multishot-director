# One-Image Multi-Shot Director

Seedance 2.5용 독립 영상 연출 스킬입니다.

한 장의 기준 이미지와 원하는 영상 길이를 입력하면, 선택한 길이에 맞춘 **통합 프롬프트 1개**를 만듭니다.

- 15초·20초·30초 또는 직접 입력한 길이 지원
- 하나의 생성 안에 4단 내부 연출 구조 설계
- 한국어 비주얼 앵커와 타임라인
- Seedance 2.5에 바로 붙여 넣는 영문 마스터 프롬프트 1개
- STORM·Notion과 독립적으로 사용

## 기본 사용 예시

> 이 인물이 달빛 아래 수호자로 각성하는 영상으로 만들어줘. 30초.

길이를 정하지 않았다면 다음 중 하나를 선택합니다.

1. 15초
2. 20초
3. 30초
4. 직접 입력

자세한 사용법은 [MANUAL.md](MANUAL.md)를 참고하세요.

## 설치

```bash
mkdir -p ~/.hermes/skills/one-image-multishot-director
cp SKILL.md ~/.hermes/skills/one-image-multishot-director/SKILL.md
```
