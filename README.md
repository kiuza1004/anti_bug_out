# 🦟 BugOut (초음파 해충 퇴치 웹앱)

웹 브라우저에서 바로 동작하는 **초음파 해충 퇴치 정적 웹 애플리케이션**입니다. 별도의 설치, 빌드 도구, 외부 의존성 없이 단일 HTML 파일(`index.html`)로 동작합니다.

**👉 웹앱 바로가기 (Live Demo):** https://kiuza1004.github.io/anti_bug_out/

---

## 🚀 주요 기능

- 🎚 **정밀 주파수 제어**: 100 Hz ~ 22,000 Hz (초음파 대역) 슬라이더 조절
- 🐛 **해충별 최적 프리셋**: 모기(18kHz), 파리(15kHz), 날파리(17kHz), 쥐(22kHz), 바퀴벌레(12kHz), 거미(20kHz)
- 🎵 **다양한 파형 지원**: Sine, Square, Sawtooth, Triangle
- 🔁 **지능형 주파수 스윕**:
  - `Slow` / `Fast`: 사인파 기반 ±1.5kHz 동적 변조
  - `Random`: 4초마다 14~22kHz 불규칙 주파수 호핑 (내성/적응 방지)
- 🎛 **맥놀이(Detune 듀얼 톤)**: 보조 오실레이터를 통한 차주파수 진폭 변조
- ⏱ **타이머 및 실시간 카운트다운**: 5분, 15분, 30분 자동 종료 및 잔여 시간 시각화
- 🔋 **화면 켜짐 유지 (Screen Wake Lock)**: 모바일 환경에서 재생 중 화면 꺼짐 방지
- 📊 **실시간 오디오 스펙트럼 시각화**: HTML5 Canvas 및 AnalyserNode 기반 주파수 막대 뷰어
- 🔉 **클릭 노이즈 방지**: 50ms Linear Ramp-in/out 적용
- ⌨️ **키보드 단축키**: Space(재생/정지), 1~6(프리셋), ↑↓(주파수 변경, Shift=1kHz), M(음소거 토글)
- 💾 **설정 자동 저장**: `localStorage`를 통해 사용자의 마지막 설정 유지

---

## 🌐 웹앱 배포 (GitHub Pages)

본 저장소의 `main` 브랜치에 코드가 푸시되면 GitHub Actions를 통해 자동으로 Pages에 배포됩니다.
- 접속 URL: `https://kiuza1004.github.io/anti_bug_out/`
- 배포 설정: **Settings → Pages → Source: `GitHub Actions`** (또는 `Deploy from a branch` → `main` / `root`)

---

## 💻 로컬 실행 방법

별도의 빌드나 의존성 설치가 필요하지 않습니다. 아무 정적 웹 서버나 브라우저로 실행할 수 있습니다.

```bash
# Python 내장 서버 사용 시
python -m http.server 8080

# 또는 Node.js npx serve 사용 시
npx serve .
```

실행 후 브라우저에서 `http://localhost:8080`으로 접속합니다.

---

## 🛠 기술 스택

- **언어**: HTML5, Vanilla JavaScript (ES6+), CSS3
- **오디오 엔진**: Web Audio API (`AudioContext`, `OscillatorNode`, `GainNode`, `AnalyserNode`)
- **디바이스 제어**: Screen Wake Lock API
- **의존성 / 라이브러리**: 0개 (외부 CDN, 프레임워크 없음)

---

## ⚠️ 주의사항

1. 초음파의 해충 퇴치 효과는 생물학적 종, 주변 환경, 기기 스피커의 물리적 출력 한계에 따라 달라질 수 있습니다.
2. 반려동물(개, 고양이, 설치류 등)은 사람보다 가청 주파수 대역이 넓어 불편함을 느낄 수 있습니다.
3. 청력이 민감한 성인이나 유아의 경우 두통이 발생할 수 있으므로, 볼륨을 낮게 시작하십시오.
4. **이어폰이나 헤드폰 착용 중에는 고음/초음파 재생을 삼가십시오.**

---

## 📄 라이선스

MIT License
