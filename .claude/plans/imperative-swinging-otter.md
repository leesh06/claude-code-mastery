# 계획: 경력 소개 포트폴리오 페이지 제작

## Context
참고 이미지 스타일의 다크 테마 포트폴리오 웹사이트를 처음부터 구축한다.
프로젝트에 HTML/CSS/JS 파일이 전혀 없으므로 모두 새로 생성한다.

## 생성할 파일
- `index.html` - 메인 페이지
- `css/style.css` - 커스텀 CSS + 애니메이션
- `js/script.js` - 인터랙션, 스크롤, 카운터 효과

## 디자인 스펙 (참고 이미지 기준)

### 색상
- 배경: `#111111` (near black)
- 서브 배경: `#1a1a1a`
- 강조색: `#ff5733` (오렌지/코랄)
- 텍스트: `#ffffff`, `#aaaaaa`

### 섹션 구성

1. **Navigation** (고정 헤더)
   - 좌: 이름/로고
   - 우: Home, About, Projects, Contact 링크 + 모바일 햄버거 메뉴

2. **Hero 섹션**
   - 좌: "Hello." (오렌지 점), "I'm [이름]", "Software Developer", 버튼 2개
   - 우: 프로필 원형 + 그라데이션 링(오렌지/레드) + 장식 < > 기호
   - 샘플 이미지: CSS 실루엣 또는 SVG 아바타 (assets 없으므로)

3. **기술 스택 마퀴 바**
   - HTML, CSS, JavaScript, Node.js, React, Git, GitHub 등 스크롤 흐름 효과

4. **About 섹션**
   - 좌: 서비스 목록 (Web Dev, App Dev, Hosting) + 아이콘 + 수직 오렌지 라인
   - 우: "About me" 제목 + 소개글 + 통계 (프로젝트수+, 만족도%, 경력년수+)

5. **Projects 섹션**
   - 카드 그리드 4개, 호버 효과

6. **Contact 섹션**
   - 이메일 폼 + 소셜 링크

## 주요 효과
- CSS 애니메이션: 페이드인, 슬라이드업
- JavaScript: Intersection Observer (스크롤 트리거)
- 카운터 애니메이션 (숫자 올라가는 효과)
- 마퀴 무한 스크롤
- 네비게이션 활성 섹션 하이라이트
- 부드러운 스크롤

## 플레이스홀더 정보
- 이름: Your Name (쉽게 교체 가능하도록 주석 표시)
- 프로필: CSS 기반 원형 아이콘 (나중에 assets/profile.jpg로 교체)

## 검증
- 브라우저에서 `index.html` 직접 열기 또는 `python -m http.server 8000`
- 모바일 반응형 확인 (Chrome DevTools)
- 모든 섹션 스크롤 애니메이션 동작 확인
