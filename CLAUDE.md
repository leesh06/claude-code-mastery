# CLAUDE.md

이 파일은 Claude Code가 이 저장소에서 작업할 때 참고하는 가이드입니다.

## 프로젝트 개요

**개발자 웹 이력서 포트폴리오**

다크 테마의 단일 페이지 포트폴리오 웹사이트. 개발자의 기술, 프로젝트, 경력을 소개합니다. 순수 HTML5, CSS3, JavaScript로만 제작되었으며, 프레임워크나 빌드 도구가 없습니다.

- **기본 언어**: 한국어 (주석, 커밋, 문서)
- **기술 스택**: HTML5 + CSS3 + Vanilla JavaScript
- **아키텍처**: 클라이언트 사이드 (백엔드 없음)
- **배포**: 정적 사이트 (GitHub Pages, Netlify, Vercel)

## 빠른 시작

### 로컬 실행
```bash
# 옵션 1: Python HTTP 서버
python -m http.server 8000

# 옵션 2: npx http-server
npx http-server .

# 옵션 3: 브라우저에서 직접 열기
# index.html을 브라우저로 열면 됨
```

그 후 `http://localhost:8000` 방문하거나 원하는 포트 사용

### 빌드 프로세스 없음
순수 프로젝트입니다. npm install, 빌드 단계, 컴파일이 전혀 필요 없습니다.

## 코드베이스 구조

### 파일 구성
```
index.html              # 단일 페이지 HTML (8개 시맨틱 섹션)
css/style.css          # 커스텀 CSS + 애니메이션 (프레임워크 없음)
js/script.js           # Vanilla JavaScript 상호작용
tailwind.config.js     # (미사용, 삭제 가능)
.claude/               # Claude Code 설정
```

### HTML 아키텍처 (`index.html`)

8개의 시맨틱 섹션으로 구성:

1. **네비게이션** - 고정 헤더
   - 좌: 로고/브랜딩
   - 우: 네비게이션 링크 (데스크톱) / 햄버거 메뉴 (모바일)

2. **히어로 섹션** - 소개 영역
   - 인사말 + 강조색 점
   - 메인 제목 (일부 하이라이트)
   - 부제목 (직급)
   - CTA 버튼 2개
   - 프로필 아바타 (이모지 + 떠있는 애니메이션)
   - 장식 꺾쇠 기호

3. **기술 스택 마퀴** - 무한 스크롤 기술 목록

4. **About 섹션** - 2열 그리드
   - 좌: 서비스 목록 (웹 개발, 앱 개발, 웹 호스팅)
   - 우: 소개글 + 통계 (카운터 애니메이션)

5. **프로젝트 섹션** - 4개 프로젝트 카드 그리드

6. **연락처 섹션** - 폼 + 소셜 미디어 링크

7. **맨 위로 가기 버튼** - 고정 버튼
   - 300px 스크롤 후 나타남
   - 클릭 시 부드럽게 상단으로 이동
   - SVG 화살표 아이콘

8. **푸터** - 저작권

### CSS 아키텍처 (`css/style.css`)

**디자인 시스템 (CSS 변수)**:
- `--bg-primary`: #111111 (메인 배경)
- `--bg-secondary`: #1a1a1a (카드 배경)
- `--accent`: #ff5733 (주황색 강조)
- `--text-primary`: #ffffff (주 텍스트)
- `--text-secondary`: #aaaaaa (보조 텍스트)
- `--transition`: all 0.3s ease (표준 전환)

**레이아웃 접근 방식**:
- CSS Grid: 다중 열 섹션 (히어로, About, 프로젝트)
- Flexbox: 네비게이션, 버튼, 소셜 링크
- 모바일 우선 반응형 설계

**주요 애니메이션**:
- `slideInLeft` / `slideInRight` - 히어로 콘텐츠 진입
- `fadeInUp` - 서비스 아이템, 프로젝트 카드 스크롤 시
- `marquee` - 기술 스택 무한 스크롤 (20초 루프)
- `floatAvatar` - 프로필 아바타 떠있는 효과 (3초 루프)

**반응형 breakpoint**:
- 데스크톱: 1200px 최대 너비
- 태블릿 (768px 이하): 단열 레이아웃, 메뉴 숨김, 햄버거 표시
- 모바일 (480px 이하): 작은 폰트, 폼 입력 세로 쌓기

### JavaScript 기능 (`js/script.js`)

**핵심 기능** (실행 순서):

1. **맨 위로 가기 버튼**
   - 300px 스크롤 임계값 기반 표시/숨김
   - 클릭 시 부드러운 스크롤 애니메이션

2. **네비게이션 활성 링크 하이라이트**
   - Intersection Observer로 현재 섹션 감지
   - 스크롤할 때 활성 네비 링크 업데이트

3. **모바일 햄버거 메뉴**
   - 클릭 시 메뉴 토글
   - 링크 클릭 시 자동 닫힘

4. **카운터 애니메이션**
   - 통계 숫자 0에서 목표값까지 애니메이션
   - 스크롤 시 트리거 (Intersection Observer)
   - 요소당 1회만 실행

5. **Intersection Observer 애니메이션**
   - 감시 대상: `.service-item`, `.stat-number`, `.project-card`
   - 동작: 스크롤 진입 시 페이드인 + 슬라이드업
   - 초기 상태: opacity: 0, translateY: 30px

6. **버튼 동작**
   - "View My Work" → 프로젝트 섹션으로 부드럽게 스크롤
   - "Get In Touch" → 연락처 섹션으로 부드럽게 스크롤

7. **폼 검증**
   - 이름: 공백 체크
   - 이메일: 정규식 검증 (`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`)
   - 메시지: 공백 체크
   - 검증 실패 시 alert 표시

8. **부드러운 스크롤 앵커**
   - 앵커 링크(#section-id) 폴백
   - 브라우저가 `scroll-behavior: smooth`를 지원하지 않으면 자동 처리

9. **페이지 로드 애니메이션**
   - 로드 시 body 페이드인
   - 시각적 폴리시

## 핵심 디자인 패턴

### 색상 시스템
모든 색상은 `:root`에서 정의된 CSS 변수 사용. 다음 6개 변수만 변경하면 테마 변경 가능:
```css
--bg-primary, --bg-secondary, --accent, --text-primary, --text-secondary, --transition
```

### 애니메이션
- 진입 애니메이션은 Intersection Observer로 트리거 (페이지 로드 시 과하지 않게)
- 모든 상호작용 요소에 부드러운 전환 (버튼, 링크, 폼 입력)
- 아바타 떠있는 효과는 연속 (3초 루프, 무한)
- 기술 스택 마퀴는 연속 (20초 루프, 무한)

### 반응형 전략
- 데스크톱: 2열 그리드 (히어로, About), 3열 통계
- 태블릿 (768px): 1열 레이아웃으로 전환, 버튼 세로 쌓기
- 모바일 (480px): 작은 텍스트, 폼 폰트 16px (Safari 자동 확대 방지)

## 중요한 구현 사항

### 폼 제출
연락처 폼은 현재 `https://formspree.io/f/your_form_id` 지정. 배포 전 다음 수정:
1. [formspree.io](https://formspree.io)에서 가입
2. 폼 생성 및 ID 획득
3. `index.html` 150번 줄의 `action` 속성 업데이트

또는 다른 이메일 서비스 사용 (Netlify Forms, SendGrid 등)

### 아바타 이미지 대체
프로필 아바타는 현재 이모지(`👨‍💻`) 사용. 실제 이미지 사용 시:
- 이모지를 `<img src="assets/profile.jpg" alt="Profile">`로 대체
- `assets/` 폴더에 이미지 추가
- 크기/스타일 조정

### 외부 의존성 없음
- jQuery, React, 빌드 도구 없음
- 최신 브라우저 지원 (Chrome, Firefox, Safari, Edge)
- CDN에서 수정 없이 배포 가능

## 공통 개발 작업

### 개인 정보 변경
HTML 전체에 다음 플레이스홀더 존재:
- "Your Name" → 실제 이름으로 변경 (로고, 히어로 제목, 푸터)
- "Software Developer" → 직급으로 변경
- Lorem ipsum → About 섹션 소개글 입력
- 이메일 및 소셜 링크 업데이트

### 스타일 수정
- 색상: `:root`의 CSS 변수 수정 (2-8줄)
- 폰트: `body` 선택자의 `font-family` 변경 (22줄)
- 간격: 섹션 클래스의 padding/margin 조정
- 애니메이션: CSS `@keyframes` 섹션에서 duration/easing 수정

### 새 섹션 추가
1. HTML에 시맨틱 `<section id="section-name">` 블록 추가
2. CSS에서 grid/flexbox로 스타일 지정
3. 네비게이션 메뉴에 링크 추가
4. JS의 Intersection Observer가 자동으로 활성 링크 업데이트

### 애니메이션 수정
- 모든 애니메이션은 CSS `@keyframes` 섹션에서 정의 (507-548줄)
- animation 단축 속성의 시간 변경 (예: `0.8s` → `1s`)
- JS의 Intersection Observer threshold/rootMargin 수정 (74-77줄)로 애니메이션 트리거 시점 조정

## 성능 관련

- 자산당 1개의 HTTP 요청 (번들링 없음)
- 총 약 50KB (HTML + CSS + JS, 압축 미포함)
- 외부 CDN 의존성 없음 (폼 제출 서비스 제외)
- Intersection Observer는 스크롤 애니메이션에 효율적 (지속적인 폴링 없음)
- 카운터 애니메이션은 `setInterval` 사용 (30ms 간격, 50 증분)

## 브라우저 지원

- 최신 브라우저: Chrome, Firefox, Safari 12+, Edge 79+
- 필수: Intersection Observer API, ES6 JavaScript
- 모바일: iOS Safari 12.2+, Android Chrome
- 우아한 하락: 구형 브라우저에서 스크롤 즉시 이동으로 대체

## 접근성

- 시맨틱 HTML5 구조
- 아이콘 버튼에 Aria 레이블 (맨 위로 가기 버튼)
- 폼 레이블과 입력 필드 적절히 연결
- 색상 대비는 WCAG AA 만족 (다크 테마 + 밝은 강조색)
- 모바일 친화적 (100vw viewport, 터치 친화적 버튼)

---

**마지막 업데이트**: 2026-03-06
