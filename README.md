# 🦟 BugOut Argon Edition (초정밀 초음파 해충 퇴치 신디사이저)

웹 브라우저에서 즉시 동작하는 **Argon 에디션 초음파 해충 퇴치 정적 웹 애플리케이션**입니다. 설치, 빌드 도구, 외부 의존성 없이 단일 HTML 파일([index.html](file:///D:/AI_Antigravity/bug_out/index.html))로 동작합니다.

**👉 웹앱 바로가기 (Live Demo):** https://kiuza1004.github.io/anti_bug_out/

---

## ⚡ Argon 에디션 주요 기능

- 🎛 **초정밀 주파수 HUD & 퀵 튜닝**:
  - 100 Hz ~ 22,000 Hz 슬라이더 및 `-1kHz`, `-100Hz`, `+100Hz`, `+1kHz` 미세 조정 버튼
  - 가청 대역 / 고주파 / 준초음파 / 초음파 대역 자동 판별 배지 및 실시간 출력 주파수 텔레메트리
- 📊 **3-모드 고해상도(DPI) 비주얼라이저**:
  - **스펙트럼 (FFT)**: 96-밴드 주파수 에너지 바 + 피크 홀드(Peak Hold) 인디케이터
  - **파형 (Waveform)**: 실시간 타임-도메인 오실로스코프 네온 파형 뷰어
  - **소나 파동 (Sonar Field)**: 초음파 방출 에너지 및 듀얼 오실레이터 간섭을 시각화하는 동심원 레이더
- 🐛 **8종 해충 맞춤 프리셋 (단축키 1~8)**:
  - 모기(18kHz), 파리(15kHz), 날파리(17kHz), 쥐·설치류(22kHz), 바퀴벌레(12kHz), 거미(20kHz), 개미(14kHz), 진드기·빈대(19.5kHz)
  - 프리셋 선택 시 최적의 **주파수 + 파형 + 스윕 + 맥놀이(Detune) + 충격 펄스**가 원클릭으로 자동 조합
- 🌊 **다중 변조 엔진 (Multi-Modulation Engine)**:
  - **파형 합성**: Sine(사인파), Square(구형파), Sawtooth(톱니파), Triangle(삼각파)
  - **주파수 스윕**: Off, Slow(±1.5kHz), Fast(±1.5kHz), Random(14~22kHz 불규칙 호핑)
  - **충격 펄스 게이트 (Pulse Gate)**: 연속파, 2Hz 버스트, 6Hz 스트로브, Chaos(불규칙 충격파)로 해충 신경계 적응 방지
  - **맥놀이 (Dual-Oscillator Detune)**: 0 ~ 100 Hz 보조 오실레이터 차주파수 간섭 생성
- 🔊 **1kHz 스피커 가청 점검**:
  - 사람 귀에 들리지 않는 초음파 출력 중 기기 스피커와 볼륨이 정상 작동하는지 즉시 확인하는 1kHz 테스트 톤 기능
- ⏱ **자동 종료 타이머 & 텔레메트리**:
  - 연속(∞), 5분, 15분, 30분, 60분 타이머 및 실시간 `MM:SS` 카운트다운
  - 모바일 화면 꺼짐 방지(Screen Wake Lock), 오디오 샘플레이트, 합성 채널 상태 실시간 표시

---

## 💻 실행 방법

1. **웹앱 바로 접속**: [https://kiuza1004.github.io/anti_bug_out/](https://kiuza1004.github.io/anti_bug_out/)
2. **로컬 실행**: [index.html](file:///D:/AI_Antigravity/bug_out/index.html) 더블 클릭 또는 정적 서버(`python -m http.server 8080`) 실행

---

## 🛠 기술 스택 및 비용

- **기술 스택**: HTML5, Vanilla JavaScript, CSS3 Glassmorphism UI, Web Audio API, Canvas 2D, Screen Wake Lock API
- **외부 의존성 / 비용**: 0개 / 0원 (100% 브라우저 내장 표준 기술)

---

## 📄 라이선스

MIT License
