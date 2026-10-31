# ANTIGRAVITY.md — BugOut Argon Edition

이 문서는 Antigravity 어시스턴트 및 개발자가 본 저장소(`BugOut Argon Edition`)를 유지보수할 때 준수해야 할 아키텍처 지침입니다.

---

## 🎯 핵심 설계 원칙

1. **단일 파일 완결성 (Single-File Architecture)**: [index.html](file:///D:/AI_Antigravity/bug_out/index.html) 한 장에 스타일(Argon Glass UI), 마크업, Web Audio 신디사이저 엔진, 3-모드 Canvas 비주얼라이저가 모두 인라인으로 포함됩니다.
2. **제로 의존성 및 제로 비용**: 외부 라이브러리, 번들러, 유료 API를 일절 사용하지 않으며 브라우저 내장 표준 API만 활용합니다.
3. **하위 호환성 보장**: `window.AudioContext || window.webkitAudioContext` 폴백 및 `navigator.wakeLock` 안전 예외 처리를 유지합니다.

---

## 🏗️ 오디오 신호 처리 그래프 (Argon Audio Pipeline)

```text
[OscillatorNode 1 (Base Freq)] ──┐
                                 ├──> [pulseGain (Pulse Gate)] ──> [gain (Master Volume)] ──> [AnalyserNode] ──> ctx.destination
[OscillatorNode 2 (Detune)] ─────┘
```

- **`osc` / `osc2`**: 주 오실레이터와 맥놀이(Detune)용 보조 오실레이터.
- **`pulseGain`**: 연속파(`off`), 2Hz 버스트(`slow`), 6Hz 스트로브(`fast`), 불규칙 게이트(`chaos`) 진폭 변조 담당.
- **`gain`**: 마스터 볼륨 및 시작/정지 시 50ms 소프트 램프(`linearRampToValueAtTime`)를 통한 클릭 팝 노이즈 억제 담당.
- **`analyser`**: FFT 크기 2048 기반 실시간 주파수(`getByteFrequencyData`) 및 타임 도메인 파형(`getByteTimeDomainData`) 추출.

---

## 💾 상태 스키마 (`localStorage: bugout:v2`)

- `freq`: 기준 주파수 (`100` ~ `22000` Hz)
- `volume`: 마스터 볼륨 (`0.0` ~ `1.0`)
- `wave`: 파형 (`sine`, `square`, `sawtooth`, `triangle`)
- `sweep`: 주파수 스윕 (`off`, `slow`, `fast`, `random`)
- `pulse`: 충격 펄스 게이트 (`off`, `slow`, `fast`, `chaos`)
- `timer`: 자동 종료 타이머 (`off`, `5`, `15`, `30`, `60`)
- `detune`: 듀얼 오실레이터 간섭 주파수 (`0` ~ `100` Hz)
- `visMode`: 캔버스 시각화 모드 (`spectrum`, `wave`, `sonar`)
- `activePreset`: 현재 선택된 해충 프리셋 ID (`mosquito`, `fly`, `gnat`, `rat`, `roach`, `spider`, `ant`, `mite`)
