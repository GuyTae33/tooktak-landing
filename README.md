# tooktak 랜딩 페이지

시공 현장 관리 PWA "tooktak" 의 홍보용 단독 사이트.

- 순수 HTML (내장 CSS / JS), 페이지 2개 구성
  - **대문(`index.html`)** — 루트 진입점. SNS·오픈채팅 프로필 링크용 인트로 화면
  - **랜딩(`home.html`)** — 서비스 소개·기능·설치법·FAQ 본문
- 외부 라이브러리·CDN·npm install 없음
- 본 앱 저장소(`C:\Users\kateb\tooktak\`)와 완전 분리 — 다른 도메인에서 호스팅

## 폴더 구조

```
tooktak-landing/
├── index.html              # 대문 페이지 (루트 진입점 — SNS 링크용)
├── home.html               # 랜딩 페이지 (서비스 소개·기능·설치법·FAQ)
├── assets/
│   ├── mockup-placeholder.svg     # 히어로 앱 목업 (1200x630 비율의 휴대폰 프레임 placeholder)
│   ├── og-image-placeholder.svg   # OG 이미지 (1200x630 placeholder)
│   └── favicon.svg                # 파비콘
├── README.md
└── .gitignore
```

## 로컬 미리보기

랜딩 페이지 폴더에서 정적 서버 하나 띄우면 됩니다.

```powershell
# Python (3.x)
python -m http.server 8000

# 또는 Node.js
npx serve .
```

VSCode 사용 시 **Live Server** 확장으로 `index.html` 우클릭 → "Open with Live Server".

브라우저: <http://localhost:8000/>

## Render Static Site 배포 가이드

> 본 앱 저장소(`tooktak`)와는 **별도 GitHub repo**로 운영하는 것을 권장. 동일 repo에 두면 자동 빌드 충돌 가능.

### 1. GitHub repo 준비

```powershell
cd C:\Users\kateb\tooktak-landing
git init
git add .
git commit -m "feat: tooktak 랜딩 페이지 초기 버전"
git branch -M main
git remote add origin https://github.com/<owner>/tooktak-landing.git
git push -u origin main
```

### 2. Render Dashboard 설정

1. <https://dashboard.render.com/> 로그인
2. 우상단 **New +** → **Static Site** 선택
3. 위에서 만든 GitHub repo (`tooktak-landing`) 연결
4. 다음 값으로 설정:

   | 항목 | 값 |
   |---|---|
   | **Name** | `tooktak-landing` (자유) |
   | **Branch** | `main` |
   | **Root Directory** | (비움 — repo 루트) |
   | **Build Command** | (비움 — 정적 파일이라 빌드 불필요) |
   | **Publish Directory** | `.` (점 하나, repo 루트) |
   | **Auto-Deploy** | `Yes` (main push 시 자동 배포) |

5. **Create Static Site** 클릭

### 3. 배포 확인

- Render가 자동으로 빌드/배포. 보통 1~3분
- 발급되는 기본 URL: `https://tooktak-landing-xxxx.onrender.com`
- 페이지 열어서 각 섹션·CTA 동작 확인

### 4. 커스텀 도메인 (선택)

1. Render Dashboard → 해당 Static Site → **Settings** → **Custom Domains**
2. 도메인 추가 (예: `tooktak.app`)
3. 안내되는 DNS 레코드(CNAME/A)를 도메인 등록기관에 등록
4. 등록 완료 시 자동으로 HTTPS 인증서 발급

> **TODO**: 실제 도메인 확정 시 `index.html` 의 `og:url`, `canonical` 주석을 활성화하고 URL 교체.

## 본 앱 저장소와의 분리 원칙

- 본 앱 코드 `C:\Users\kateb\tooktak\` 는 **읽기 외 일절 수정·복사·이동 금지**
- 랜딩 페이지에서 본 앱으로의 진입은 외부 링크 (`https://tooktakproject.web.app/`)로만
- service worker · manifest.json 생성 금지 (도메인이 다르므로 PWA 충돌 방지)

## 향후 교체 필요 placeholder

| 위치 | 내용 |
|---|---|
| `index.html` / `home.html` `og:url`, `canonical` 주석 | 실제 배포 도메인 |
| `assets/og-image-placeholder.svg` | 실제 OG 이미지(1200x630 PNG/JPG 권장) |
| `assets/mockup-placeholder.svg` | 실제 앱 스크린샷 목업 |
| `assets/favicon.svg` | 실제 파비콘 (브랜드 로고) |

### 처리 완료 / 보류

- 문의 이메일: `mailto:rumanesystem@gmail.com` 연결 완료
- 오픈채팅: `https://open.kakao.com/o/pOhG91vi` 연결 완료
- 개인정보처리방침: 정책 문서 미확정 — 푸터 링크·FAQ 언급 **임시 제거**. 정책 확정 시 푸터 "문의" 영역에 링크 재추가 필요
- 운영팀/사업자 정보: 푸터 항목 **제거** (무료 홍보 페이지). 향후 유료화 시 전자상거래법상 사업자정보 표기 재검토 필요

> 하단 CTA 오픈채팅 링크는 `https://open.kakao.com/o/pOhG91vi` 로 연결 완료.
