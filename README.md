# 🌌 우주 천체 궤도 시뮬레이션 앱

**버전**: 1.0.0  
**라이선스**: MIT  
**최종 업데이트**: 2024년  

---

## 📚 개요

우주를 거리와 크기 단위별로 시각적으로 이해할 수 있는 인터랙티브 교육 앱입니다.

### 🎯 주요 기능

| 기능 | 설명 |
|------|------|
| **📍 크기 비교** | 천체들의 상대 크기를 시각적으로 비교 |
| **🌍 거리 탐색** | 줌 기능으로 우주의 다양한 스케일 체험 |
| **🛰️ 궤도 시뮬레이션** | 뉴턴의 물리 법칙으로 실제 궤도 계산 및 충돌 시뮬레이션 |
| **📐 단위 설명** | 거리/크기 단위 설명 및 변환기 |
| **🎮 3D 뷰** | Three.js로 천체를 3D로 표현 |

---

## 🚀 빠른 시작

### 1. 설치

```bash
# 프로젝트 디렉토리 이동
cd universe-app

# 의존성 설치
npm install
```

### 2. 개발 서버 실행

```bash
# 브라우저 자동 열기
npm run dev

# 또는 수동으로
npm start

# 접속 URL: http://localhost:3000
```

### 3. 프로덕션 빌드

```bash
# 최적화된 빌드
npm run build

# 결과물: dist/ 폴더
```

### 4. 배포

자세한 배포 가이드는 [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) 참조

---

## 📋 프로젝트 구조

```
universe-app/
├── public/
│   └── index.html                    # 메인 HTML
├── src/
│   ├── components/
│   │   ├── SizeComparison.jsx        # 크기 비교 탭
│   │   ├── DistanceExplorer.jsx      # 거리 탐색 탭
│   │   ├── OrbitalSimulation.jsx     # 궤도 시뮬레이션 탭
│   │   ├── UnitsGuide.jsx            # 단위 설명 탭
│   │   └── CelestialBody3D.jsx       # 3D 뷰 탭
│   ├── data/
│   │   ├── celestialData.js          # 천체 데이터 (13개)
│   │   └── units.js                  # 거리/크기 단위 정의
│   ├── utils/
│   │   └── physics.js                # 뉴턴 물리 엔진
│   ├── App.jsx                       # 메인 앱 컴포넌트
│   └── index.js                      # 진입점
├── webpack.config.js                # Webpack 설정
├── package.json                     # 의존성 및 스크립트
├── DEPLOYMENT_GUIDE.md              # 배포 & 테스트 가이드
└── README.md                        # 본 파일

```

---

## 🔧 기술 스택

| 분야 | 기술 |
|------|------|
| **프론트엔드** | React 19.2.5 |
| **3D 렌더링** | Three.js r128 |
| **번들링** | Webpack 5.106 |
| **스타일** | 인라인 CSS + Tailwind |
| **빌드 도구** | Babel, webpack-dev-server |

---

## 🎮 사용 가이드

### 📍 크기 비교

1. 슬라이더로 천체 선택
2. 두 천체의 상대 크기 비교
3. 크기 단위 변환 (km, R⊕, R☉)
4. 흥미로운 사실 학습
5. "3D 천체 보기" 클릭으로 3D 뷰 전환

### 🌍 거리 탐색

1. 줌 슬라이더로 우주 스케일 조정
2. 현재 스케일 단위 자동 변환
3. 거리 단위 선택 (km, AU, 광년 등)
4. SVG 시각화에서 천체 위치 확인
5. 천체 클릭으로 상세 정보 확인

### 🛰️ 궤도 시뮬레이션

1. **시나리오 선택**:
   - 태양계 (8행성)
   - 지구-달 시스템
   - 태양-지구
   - 3체 문제 (카오스)

2. **시뮬레이션 제어**:
   - ▶️ 재생 / ⏸️ 정지
   - 🔄 리셋
   - 속도 0.1x ~ 10x 조절

3. **시각화 옵션**:
   - ☑️ 흔적 표시 (궤도 궤적)
   - ☑️ 레이블 표시 (천체명)

4. **통계 모니터링**:
   - 천체 수
   - 충돌 횟수
   - 시뮬레이션 경과 시간

### 📐 단위 설명

1. **거리 단위**:
   - 미터 (m)
   - 킬로미터 (km)
   - 천문단위 (AU)
   - 광년 (ly)
   - 파섹 (pc)

2. **크기 단위**:
   - 킬로미터 (km)
   - 지구반경 (R⊕)
   - 태양반경 (R☉)

3. **변환기**:
   - 거리 변환
   - 크기 변환
   - 실시간 계산

### 🎮 3D 뷰

1. **마우스 조작**:
   - 드래그: 천체 회전
   - 휠: 줌 인/아웃

2. **자동 회전**: 토글로 온/오프

3. **상세 정보**:
   - 물리 속성 (반지름, 질량, 밀도, 온도)
   - 궤도 정보
   - 흥미로운 사실 (5개)

---

## 📊 천체 데이터

### 포함된 천체 (총 13개)

**행성 (8개)**
- ☀️ 태양 (별)
- ☿️ 수성
- ♀️ 금성
- 🌍 지구
- 🌙 달 (위성)
- ♂️ 화성
- ♃ 목성
- ♄ 토성
- ♅ 천왕성
- ♆ 해왕성

**항성 (3개)**
- ⭐ 시리우스 (가장 밝은 별)
- ⭐ 폴라리스 (북극성)
- ⭐ 베가 (직녀)

### 데이터 소스

- NASA 공개 데이터
- JPL (Jet Propulsion Laboratory)
- ESA (European Space Agency)
- 천문학 참고 자료

---

## 🔬 물리 엔진 구현

### 뉴턴의 중력 법칙

```
F = G × m₁ × m₂ / r²
a = F / m
```

### 수치 적분 (Velocity Verlet)

```javascript
// 각 시간 스텝:
1. 가속도 계산 (모든 천체의 중력 영향)
2. 속도 업데이트: v += a × dt
3. 위치 업데이트: x += v × dt
```

### 충돌 감지

```javascript
// 거리 기반 충돌:
distance < radius₁ + radius₂

// 충돌 시 병합 (운동량 & 질량 보존):
m_new = m₁ + m₂
v_new = (m₁v₁ + m₂v₂) / m_new
x_new = (m₁x₁ + m₂x₂) / m_new
r_new = ∛(r₁³ + r₂³)
```

---

## 📈 성능 스펙

| 항목 | 값 |
|------|-----|
| **초기 로딩 시간** | < 2초 |
| **번들 크기** | 748 KiB (압축됨) |
| **메모리 사용** | ~ 100MB |
| **FPS** | 60 FPS (Chrome/Firefox) |
| **최대 천체 수** | 20+ (성능 저하 주의) |

---

## 🐛 알려진 이슈

### 현재 없음 ✅

버그나 개선사항을 발견하면 [이슈 제출](https://github.com/yourusername/universe-app/issues)해주세요.

---

## 🔮 향후 계획

- [ ] 행성 텍스처 이미지 추가
- [ ] 실제 천문 데이터 업데이트
- [ ] 행성 찾기 게임
- [ ] 다국어 지원
- [ ] 모바일 앱 (React Native)
- [ ] VR 모드 (Three.js WebXR)
- [ ] 사용자 저장/공유 기능
- [ ] 실시간 천문 이벤트 알림

---

## 🤝 기여하기

1. Fork 하기
2. Feature 브랜치 생성 (`git checkout -b feature/AmazingFeature`)
3. Commit (`git commit -m 'Add AmazingFeature'`)
4. Push (`git push origin feature/AmazingFeature`)
5. Pull Request 생성

---

## 📜 라이선스

MIT License - [LICENSE](./LICENSE) 파일 참조

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 📞 연락처

- **이메일**: your.email@example.com
- **GitHub**: [@yourusername](https://github.com/yourusername)
- **블로그**: [Your Blog](https://yourblog.com)

---

## 🙏 감사의 말

- React 팀 (프론트엔드 프레임워크)
- Three.js 커뮤니티 (3D 렌더링)
- NASA & ESA (천문 데이터)
- 모든 기여자들

---

## 📚 참고 자료

### 과학 참고서
- [NASA 우주 과학](https://science.nasa.gov/)
- [Wikipedia 천문학](https://en.wikipedia.org/wiki/Astronomy)
- [Stellarium](https://stellarium.org/) - 천문 시뮬레이터

### 기술 가이드
- [React 공식 문서](https://react.dev)
- [Three.js 튜토리얼](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene)
- [Webpack 가이드](https://webpack.js.org/guides/)

### 배포 가이드
- [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) - 상세 배포 & 테스트 가이드

---

## 🎓 학습 목표

이 프로젝트를 통해 학습할 수 있는 것들:

- ✅ React 고급 패턴 (상태 관리, 성능 최적화)
- ✅ Three.js 기초 (3D 렌더링, 마우스 상호작용)
- ✅ 물리 엔진 구현 (뉴턴의 법칙, 수치 적분)
- ✅ Webpack 설정 및 최적화
- ✅ 과학 데이터 시각화
- ✅ 웹 앱 배포 및 호스팅

---

**Happy Exploring! 🚀🌌**
