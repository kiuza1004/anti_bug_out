# ANTIGRAVITY.md

이 문서는 Antigravity 어시스턴트 및 개발자가 본 저장소의 코드를 유지보수하고 확장할 때 준수해야 할 핵심 지침을 제공합니다.

---

## 🎯 프로젝트 철학

- **단일 파일 원칙 (Single File Delivery)**: `index.html` 단 한 장이 곧 전체 앱이자 배포 산출물입니다.
- **제로 의존성 (Zero Dependencies)**: 빌드 도구, 번들러, NPM 패키지, 프레임워크(React, Vue 등)를 도입하지 않습니다.
- **최대 호환성 및 제로 비용**: 브라우저 표준 내장 API(Web Audio API, Screen Wake Lock API, Canvas 2D)만 사용하며 일체의 유료 서비스나 서버를 요구하지 않습니다.

---

## 🏗️ 아키텍처 구조 (`index.html`)

1. **상태 관리 (`state` & `INITIAL_STATE`)**:
   - `freq`: 주파수 (100 ~ 22000 Hz)
   - `volume`: 볼륨 (0.0 ~ 1.0)
   - `wave`: 파형 (`sine`, `square`, `sawtooth`, `triangle`)
   - `sweep`: 스윕 모드 (`off`, `slow`, `fast`, `random`)
   - `timer`: 타이머 설정 (`off`, `5`, `15`, `30`)
   - `detune`: 듀얼 오실레이터 주파수 차이 (0 ~ 100 Hz)
   - `activePreset`: 활성 프리셋 ID
   - `playing`: 재생 여부 불리언

2. **Web Audio 그래프**:
   ```
   [OscillatorNode (Primary)] ───┐
                                 ├───> [GainNode] ───> [AnalyserNode] ───> ctx.destination
   [OscillatorNode (Detune)] ────┘
   ```
   - 클릭 팝 노이즈 방지: 시작/종료 시 50ms의 `linearRampToValueAtTime` 적용 필수.
   - 듀얼 오실레이터: `detune > 0`일 때만 생성되어 차주파수 맥놀이를 유도.

3. **스윕 및 타이머 메커니즘**:
   - `slow` / `fast`: `Math.sin` 함수로 삼각함수 기반 부드러운 주파수 변조 (기본 ±1.5kHz).
   - `random`: 4초 주기 14~22kHz 랜덤 호핑으로 곤충의 주파수 적응 방지.
   - `timer`: 1초 단위 카운트다운 인터벌을 통해 UI에 실시간 잔여 시간(MM:SS) 렌더링.

4. **디바이스 제어**:
   - `navigator.wakeLock`: 재생 중 모바일 기기 화면이 꺼지는 것을 방지.
   - `document.visibilitychange`: 브라우저 탭이 백그라운드로 전환될 경우 배터리 및 오디오 리소스 보존을 위해 자동 정지.

5. **영속성 (`localStorage`)**:
   - 키: `bugout:v1`
   - 컨트롤 변경 시 실시간 저장, 페이지 로드 시 1회 복원.

---

## 📋 규칙 및 개발 가이드라인

- **새 컨트롤/옵션 추가 시 절차**:
  1. `index.html` 내 마크업 및 스타일 정의
  2. `INITIAL_STATE`에 기본값 등록
  3. `saveState()` 및 `loadState()`에 필드 반영
  4. `render()` 함수에 DOM 상태 동기화 추가
  5. 런타임 오디오 그래프(`ctx`, `osc`, `gain`) 동적 업데이트 로직 연결
- **주파수 한계선**:
  - 상한: 22,000 Hz (표준 44.1/48kHz 오디오 샘플레이트의 나이퀴스트 주파수 한계 고려).
  - 하한: 100 Hz.
