# 🚀 우주 천체 궤도 시뮬레이션 앱 - 배포 & 테스트 가이드

## 📋 목차
1. [로컬 개발 환경 설정](#1-로컬-개발-환경-설정)
2. [개발 서버 실행](#2-개발-서버-실행)
3. [테스트 프로세스](#3-테스트-프로세스)
4. [프로덕션 빌드](#4-프로덕션-빌드)
5. [배포 옵션](#5-배포-옵션)
6. [트러블슈팅](#6-트러블슈팅)

---

## 1. 로컬 개발 환경 설정

### 1-1. 필수 요구사항
```
- Node.js 14.0 이상
- npm 6.0 이상 (또는 yarn)
- Git (선택사항)
- 최신 웹 브라우저 (Chrome, Firefox, Safari, Edge)
```

### 1-2. 환경 확인
```bash
# Node.js 버전 확인
node --version

# npm 버전 확인
npm --version
```

### 1-3. 프로젝트 폴더 구조

```
universe-app/
├── public/
│   └── index.html              # 메인 HTML 파일
├── src/
│   ├── components/
│   │   ├── SizeComparison.jsx   # 크기 비교 탭
│   │   ├── DistanceExplorer.jsx # 거리 탐색 탭
│   │   ├── OrbitalSimulation.jsx # 궤도 시뮬레이션 탭
│   │   ├── UnitsGuide.jsx       # 단위 설명 탭
│   │   └── CelestialBody3D.jsx  # 3D 뷰 탭
│   ├── data/
│   │   ├── celestialData.js    # 천체 데이터
│   │   └── units.js             # 단위 정의
│   ├── utils/
│   │   └── physics.js           # 물리 엔진
│   ├── App.jsx                 # 메인 앱 컴포넌트
│   └── index.js                # 진입점
├── webpack.config.js           # Webpack 설정
├── package.json               # 의존성 정의
└── dist/                       # 빌드 결과물 (자동 생성)
```

### 1-4. 의존성 설치

```bash
# 프로젝트 디렉토리 이동
cd universe-app

# npm을 사용한 설치 (권장)
npm install

# 또는 yarn을 사용한 설치
yarn install

# 설치 확인
npm ls
```

---

## 2. 개발 서버 실행

### 2-1. 개발 모드 시작 (권장)

```bash
# 자동으로 브라우저 열기
npm run dev

# 또는 수동으로 시작
npm start

# 터미널 출력:
# > universe-app@1.0.0 start
# > webpack serve --mode development
# 
# <s> [webpack-dev-server] Project is running at:
# <s> [webpack-dev-server] http://localhost:3000/
```

### 2-2. 브라우저에서 확인

- URL: `http://localhost:3000/`
- 자동 핫 리로드 활성화 (코드 변경 시 자동 새로고침)

### 2-3. 개발 서버 중지

```bash
Ctrl + C  # 또는 Command + C (Mac)
```

---

## 3. 테스트 프로세스

### 3-1. 기능별 테스트

#### **탭 1: 크기 비교 📍**

**테스트 항목:**
- [ ] 슬라이더로 다른 천체 선택 가능
- [ ] 두 천체의 상대 크기 정확히 표시
- [ ] 크기 단위 (km, R⊕, R☉) 정확히 변환
- [ ] 천체 정보 패널 데이터 정확
- [ ] "3D 천체 보기" 버튼 클릭 시 3D 뷰로 이동
- [ ] 흥미로운 사실 표시

**테스트 사례:**
```
1. 태양과 지구 비교
   - 태양이 지구보다 훨씬 커야 함
   - 반지름 값: 태양 696,000km vs 지구 6,371km

2. 금성과 수성 비교
   - 금성이 수성보다 약간 더 커야 함
   - 크기 단위 변환 정확성 확인

3. 3D 버튼 클릭
   - 선택된 천체의 3D 뷰가 표시되어야 함
```

#### **탭 2: 거리 탐색 🌍**

**테스트 항목:**
- [ ] 줌 슬라이더 0~100% 정상 작동
- [ ] 스케일 단위 자동 변환 (m → km → AU → 광년)
- [ ] 거리 단위 선택 정상 작동
- [ ] SVG 시각화 천체 위치 정확
- [ ] 거리 수치 정확
- [ ] 천체 클릭 시 3D 뷰로 이동

**테스트 사례:**
```
1. 줌 레벨 50 (중간)
   - 스케일이 적절하게 표시되어야 함
   - 대부분의 행성이 보여야 함

2. 줌 레벨 0 (최소)
   - 태양만 크게 보여야 함
   - 단위: 미터 (m)

3. 줌 레벨 100 (최대)
   - 전체 우주 스케일
   - 행성들이 거의 가시화되지 않아야 함

4. 단위 변환
   - 1 AU = 0.0000 ly?
   - 거리 테이블의 수치와 일치하는지 확인
```

#### **탭 3: 궤도 시뮬레이션 🛰️** (가장 중요!)

**테스트 항목:**
- [ ] 시나리오 로드 정상 작동
- [ ] 재생/정지 버튼 작동
- [ ] 속도 제어 슬라이더 0.1x ~ 10x 작동
- [ ] 천체가 원형 궤도를 따라 움직임
- [ ] 리셋 버튼으로 시뮬레이션 초기화
- [ ] 흔적 토글 정상 작동
- [ ] 레이블 토글 정상 작동
- [ ] 통계 정보 업데이트
- [ ] 충돌 감지 및 천체 병합 작동

**테스트 사례:**

```
1. 태양계 시나리오
   - 8개 행성이 태양 중심으로 궤도
   - 시간 경과에 따라 행성 위치 변화
   - 충돌 없어야 함 (장기 안정성 테스트)

2. 지구-달 시스템
   - 달이 지구 주위를 원형 궤도로 공전
   - 주기가 약 27일에 해당해야 함

3. 충돌 시뮬레이션 (3체 문제)
   - 충돌 감지 발생
   - 두 천체가 병합됨
   - 천체 수 감소 (N → N-1)
   - 통계에 충돌 카운트 증가

4. 속도 제어
   - 0.1x: 매우 느린 속도 (초당 이동 명백)
   - 1x: 정상 속도
   - 5x: 빠른 속도 (궤도 빠르게 완성)
   - 10x: 최대 속도 (즉시 행성 위치 변화)

5. 흔적 표시
   - ON: 각 천체 뒤에 궤적 선이 그려짐
   - OFF: 궤적이 표시되지 않음
```

**물리 검증:**
```
1. 궤도 안정성
   - 중심별 주위를 도는 행성의 궤도가 일정해야 함
   - 시간이 지나도 궤도가 붕괴되지 않음 (수치 안정성)

2. 충돌 물리
   - 충돌 후 질량 보존: m_new = m1 + m2
   - 운동량 보존: p_new = p1 + p2
   - 위치: 질량 중심

3. 에너지 보존 (선택사항)
   - 충돌이 없을 경우, 총 에너지가 일정해야 함
   - 작은 수치 오차는 예상됨
```

#### **탭 4: 단위 설명 📐**

**테스트 항목:**
- [ ] 거리 단위 설명 정확
- [ ] 크기 단위 설명 정확
- [ ] 거리 변환기 정상 작동
- [ ] 크기 변환기 정상 작동
- [ ] 변환 결과 수학적 정확성

**테스트 사례:**
```
1. 거리 변환
   - 1 km = 1,000 m
   - 1 AU = 149,600,000 km
   - 1 광년 = 9.461 × 10^12 km

2. 크기 변환
   - 1 R⊕ = 6,371 km
   - 1 R☉ = 696,000 km

3. 역함수 변환
   - 1 km → m → km (같은 값으로 돌아와야 함)
```

#### **탭 5: 3D 뷰 🎮**

**테스트 항목:**
- [ ] 천체가 3D 구로 렌더링됨
- [ ] 마우스 드래그로 회전 가능
- [ ] 마우스 휠로 줌 인/아웃 가능
- [ ] 자동 회전 토글 정상 작동
- [ ] 천체별 색상 정확
- [ ] 정보 패널 데이터 정확
- [ ] 흥미로운 사실 표시

**테스트 사례:**
```
1. 태양 (Sun)
   - 색상: 황금색 (#FDB813)
   - 흰색 자동 회전 (태양 자전)
   - 정보: 질량, 밀도 등 정확

2. 지구 (Earth)
   - 색상: 파란색 (#4A90E2)
   - 자동 회전 24시간 주기
   - 흥미로운 사실: "유일하게 생명이 존재하는 행성입니다"

3. 큰 가스 거인 (목성/토성)
   - 3D 렌더링이 부드러워야 함
   - 회전 속도가 현실적이어야 함

4. 마우스 상호작용
   - 드래그: 천체 회전 (물리적으로 자연스러움)
   - 휠: 거리 변화 (부드러운 줌)
```

---

## 4. 프로덕션 빌드

### 4-1. 빌드 실행

```bash
# 프로덕션 빌드 (최적화, 미니피케이션)
npm run build

# 터미널 출력:
# > universe-app@1.0.0 build
# > webpack --mode production
# 
# asset bundle.js 748 KiB [emitted] [minimized] [big]
# asset index.html 587 bytes [emitted]
# webpack 5.106.2 compiled successfully
```

### 4-2. 빌드 결과 확인

```bash
# dist 폴더 생성 확인
ls -la dist/

# 파일 크기 확인
du -sh dist/

# 파일 내용 확인
ls -lh dist/
```

**예상 출력:**
```
dist/
├── bundle.js      # 748 KiB (메인 코드)
└── index.html     # 587 bytes (HTML 진입점)
```

### 4-3. 로컬에서 빌드 테스트

```bash
# Python 3 웹 서버 (권장)
cd dist
python3 -m http.server 8000

# Python 2 웹 서버
python -m SimpleHTTPServer 8000

# Node.js http-server (설치 필요)
npx http-server dist -p 8000

# 브라우저에서 확인
# http://localhost:8000
```

---

## 5. 배포 옵션

### 5-1. GitHub Pages (무료)

#### **장점:**
- 완전 무료
- GitHub 계정만 필요
- HTTPS 자동 제공
- 유지보수 쉬움

#### **단계별 가이드:**

**Step 1: GitHub 저장소 생성**
```bash
# GitHub에서 새 저장소 생성 (예: universe-app)
# 또는 기존 저장소 사용

# 로컬 폴더에서 초기화
git init
git add .
git commit -m "Initial commit: Universe App"
```

**Step 2: package.json 수정**
```json
{
  "homepage": "https://yourusername.github.io/universe-app",
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

**Step 3: gh-pages 설치**
```bash
npm install --save-dev gh-pages
```

**Step 4: 배포**
```bash
npm run deploy

# 또는 수동으로
git push origin main
```

**Step 5: GitHub 설정**
- GitHub → Settings → Pages
- Source: gh-pages branch
- 몇 분 후 `https://yourusername.github.io/universe-app`에서 접속 가능

### 5-2. Netlify (권장)

#### **장점:**
- 무료 호스팅
- 자동 배포 (Git 연동)
- 환경 변수 지원
- 분석 기능 제공

#### **배포 가이드:**

**Step 1: Netlify 가입**
- https://netlify.com 접속
- GitHub 계정으로 로그인

**Step 2: 저장소 연동**
```
1. New site from Git 클릭
2. GitHub 저장소 선택
3. Build settings 설정:
   - Build command: npm run build
   - Publish directory: dist
4. Deploy site 클릭
```

**Step 3: 환경 변수 (선택사항)**
```
Site settings → Build & deploy → Environment
변수 추가: NODE_ENV = production
```

**자동 배포 설정:**
```
- 모든 git push가 자동으로 배포됨
- Pull Request는 preview로 생성됨
```

### 5-3. Vercel (권장)

#### **장점:**
- Next.js 최적화
- 매우 빠른 배포
- Edge 함수 지원
- 무료 호스팅

#### **배포 가이드:**

```bash
# Vercel CLI 설치
npm i -g vercel

# 배포
vercel

# 또는 웹에서
1. vercel.com 접속
2. GitHub 계정 연동
3. 저장소 선택
4. 자동 배포
```

### 5-4. AWS S3 + CloudFront

#### **장점:**
- 글로벌 CDN
- 매우 빠름
- 확장성 좋음

#### **배포 가이드:**

```bash
# 1. AWS CLI 설치 및 설정
aws configure

# 2. S3 버킷 생성
aws s3 mb s3://universe-app-bucket

# 3. 빌드
npm run build

# 4. S3 배포
aws s3 sync dist/ s3://universe-app-bucket/ --delete

# 5. CloudFront 설정 (AWS Console)
# - S3 버킷 선택
# - 배포 생성
# - 캐시 정책 설정

# 접속 URL: CloudFront 도메인
```

### 5-5. Docker를 사용한 배포

#### **Dockerfile 생성:**

```dockerfile
# 빌드 스테이지
FROM node:18-alpine as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# 런타임 스테이지
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

#### **배포:**

```bash
# 빌드
docker build -t universe-app .

# 로컬 테스트
docker run -p 8000:80 universe-app

# Docker Hub에 푸시
docker tag universe-app yourusername/universe-app
docker push yourusername/universe-app

# Heroku, AWS ECS, Google Cloud Run 등에 배포 가능
```

---

## 6. 트러블슈팅

### 6-1. 포트 3000이 이미 사용 중

```bash
# 포트 찾기 (macOS/Linux)
lsof -i :3000

# 프로세스 종료
kill -9 <PID>

# 다른 포트 사용
webpack serve --mode development --port 3001
```

### 6-2. Node 모듈 오류

```bash
# 의존성 재설치
rm -rf node_modules package-lock.json
npm install

# 캐시 삭제
npm cache clean --force
npm install
```

### 6-3. 메모리 부족

```bash
# Node 메모리 증가
NODE_OPTIONS=--max-old-space-size=4096 npm run build
```

### 6-4. 3D 렌더링이 느림

```
- 브라우저 하드웨어 가속 활성화
- Three.js 설정 최적화:
  * 기하학 세분화 감소 (SphereGeometry의 32 사용)
  * 텍스처 사용 비활성화 (단색 사용)
```

### 6-5. 빌드 크기 너무 큼 (748 KiB)

```bash
# 1. 코드 분할
npm install --save-dev @babel/plugin-syntax-dynamic-import

# 2. Tree shaking 활성화 (이미 활성화됨)

# 3. Three.js 최소화
import * as THREE from 'three';
// 대신
import { Scene, Camera, Renderer } from 'three';

# 4. 압축 확인
npm run build -- --analyze
```

---

## 7. 성능 최적화 팁

### 7-1. 개발 중

```bash
# 빠른 개발 서버 시작
npm start

# 메모리 사용 모니터링
node --inspect node_modules/.bin/webpack serve

# Chrome DevTools에서 성능 프로파일링
```

### 7-2. 프로덕션

```
1. 정적 파일 압축 활성화
2. CDN 사용
3. 캐시 헤더 설정
4. 이미지 최적화
5. 코드 분할
```

### 7-3. 브라우저 최적화

```javascript
// requestAnimationFrame 사용 (이미 구현됨)
// 불필요한 리렌더링 방지
// 메모리 누수 확인
```

---

## 8. 모니터링 & 로깅

### 8-1. 에러 추적

```bash
# 브라우저 콘솔에서 에러 확인
# F12 → Console 탭

# 프로덕션에서 Sentry 사용
npm install @sentry/react

# Sentry 설정 (App.jsx)
import * as Sentry from "@sentry/react";

Sentry.init({
  dsn: "YOUR_DSN",
  environment: "production"
});
```

### 8-2. 성능 측정

```bash
# Lighthouse 사용 (Chrome DevTools)
# F12 → Lighthouse → Generate report

# PageSpeed Insights
# https://pagespeed.web.dev/

# WebPageTest
# https://www.webpagetest.org/
```

---

## 9. 체크리스트

### 배포 전 최종 확인

- [ ] 모든 기능이 작동하는가?
- [ ] 콘솔에 에러가 없는가?
- [ ] 반응형 디자인 테스트 완료?
- [ ] 다양한 브라우저에서 테스트?
- [ ] 3D 렌더링이 부드러운가?
- [ ] 성능이 만족스러운가? (로딩 < 2초)
- [ ] SEO 메타 태그 추가?
- [ ] 개인정보보호정책 페이지?
- [ ] 사용 가능 여부 확인?
- [ ] 백업 생성?

---

## 10. 추가 리소스

### 공식 문서
- [React 공식 문서](https://react.dev)
- [Three.js 공식 문서](https://threejs.org/docs)
- [Webpack 공식 문서](https://webpack.js.org)
- [Node.js 공식 문서](https://nodejs.org/docs)

### 배포 가이드
- [GitHub Pages](https://pages.github.com/)
- [Netlify Docs](https://docs.netlify.com/)
- [Vercel Docs](https://vercel.com/docs)
- [AWS Hosting](https://aws.amazon.com/getting-started/hands-on/)

### 커뮤니티
- [React Community](https://react.dev/community/resources)
- [Three.js Forum](https://discourse.threejs.org/)
- [Webpack Discussion](https://github.com/webpack/webpack/discussions)

---

**마지막 업데이트**: 2024년
**버전**: 1.0.0
**라이선스**: MIT
