# 1. 도서관 관리 시스템(Library Management System, LMS) 요구사항 명세서

## 1.1 프로젝트 개요

- 프로젝트명: 도서관 관리 시스템(Library Management System, LMS)
- 개발 기간 3일(18시간)
- 개발 환경: Django, Python, SQLite, Bootstrap(선택사항)

## 1.2 프로젝트 설명

도서관 관리 시스템(Library Management System, LMS)은 도서관의 도서 및 회원 정보를 관리하는 시스템입니다.

## 1.3 프로젝트 기능

### 1.3.1 사용자 관리
1. 사용자 유형
    - 사서(Librarian): 도서 및 회원 정보 관리
    - 일반 사용자(User): 도서 대출, 반납 및 예약
2. 인증 기능
    - 회원가입(이메일, 비밀번호)
    - 로그인, 로그아웃

### 1.3.2 도서 관리
1. 도서 정보
    - 도서명, 저자, ISBN, 출판사
    - 전체 수량, 대출 가능 수량
    - 도서 상태(대출 중, 대출 가능)
    - 도서 등록, 수정, 삭제(사서 전용)
    - 도서 목록 출력
2. 도서 검색 (선택 사항)
    - 도서명 또는 저자로 검색
    - ISBN으로 검색
    - 검색 결과 목록 출력
    - 도서 상세 정보 확인
    - 검색 결과 페이징

### 1.3.3 대출/반납 시스템
1. 대출 관리
    - 도서 대출
    - 1인당 최대 3권 대출 가능
    - 대출 기간 (14일)
    - 연체 시 추가 대출 제한
2. 반납 관리
    - 도서 반납
    - 연체일 수 계산
    - 반납 시 예약자 우선 순위 처리 (선착순)

### 1.3.4 예약 시스템
1. 도서 예약 규칙
    - 대출 중인 도서 예약 불가
    - 1인당 도서별 1회 예약 가능
    - 예약 유효기간 (1일)

## 1.4 프로젝트 구조

프로젝트 구조는 다음과 같이 구성합니다.
```
lms_project/
    ├── manage.py                   # Django 관리 명령어
    ├── db.sqlite3                  # SQLite 데이터베이스 파일
    │
    ├── config/                     # 프로젝트 설정 폴더
    │   ├── init.py
    │   ├── asgi.py                # ASGI 설정
    │   ├── settings.py           # 프로젝트 설정
    │   ├── urls.py              # 프로젝트 URL 설정
    │   └── wsgi.py             # WSGI 설정
    │
    ├── static/                     # 정적 파일
    │   ├── css/                  # CSS 파일
    │   └── js/                  # JavaScript 파일
    │
    ├── templates/                  # 공통 템플릿
    │   ├── base.html              # 기본 템플릿
    │   └── navbar.html            # 네비게이션 바
    │
    ├── accounts/                   # 사용자 관리 앱
    │   ├── migrations/
    │   ├── templates/             # 사용자 관리 템플릿
    │   │   └── accounts/         # accounts 앱 템플릿
    │   │       ├── login.html   # 로그인
    │   │       ├── register.html # 회원가입
    │   │       └── profile.html # 프로필
    │   ├── init.py 
    │   ├── admin.py # 사용자 관리 관리자 설정
    │   ├── apps.py 
    │   ├── forms.py # 사용자 폼
    │   ├── models.py # 사용자 모델
    │   ├── urls.py # 사용자 URL 설정
    │   └── views.py # 사용자 뷰
    │
    └── books/                      # 도서 관리 앱
        ├── migrations/ 
        ├── templates/             # 도서 관리 템플릿
        │   └── books/            # books 앱 템플릿
        │       ├── book_list.html # 도서 목록
        │       ├── book_detail.html # 도서 상세
        │       ├── loan_list.html # 대출 목록
        │       └── reservation_list.html # 예약 목록
        ├── init.py
        ├── admin.py # 도서 관리 관리자 설정
        ├── apps.py 
        ├── forms.py # 도서 폼
        ├── models.py # 도서 모델
        ├── urls.py # 도서 URL 설정
        └── views.py # 도서 뷰
```
### 1.4.1 프로젝트 구조 설명

1. `lms_project/`: 프로젝트 폴더
2. `manage.py`: Django 관리 명령어
3. `db.sqlite3`: SQLite 데이터베이스 파일
4. `config/`: 프로젝트 설정 폴더
    - `settings.py`: 프로젝트 설정
    - `urls.py`: 프로젝트 URL 설정
    - `wsgi.py`: WSGI 설정
    - `asgi.py`: ASGI 설정
5. `static/`: 정적 파일
    - `css/`: CSS 파일
    - `js/`: JavaScript 파일
6. `templates/`: 공통 템플릿
    - `base.html`: 기본 템플릿
    - `navbar.html`: 네비게이션 바
7. `accounts/`: 사용자 관리 앱
    - `models.py`: 사용자 모델
    - `forms.py`: 사용자 폼
    - `views.py`: 사용자 뷰
    - `urls.py`: 사용자 URL 설정
    - `admin.py`: 사용자 관리 관리자 설정
    - `templates/accounts/`: 사용자 관리 템플릿
    - `migrations/`: 마이그레이션 파일
    - `apps.py`: 앱 설정
8. `books/`: 도서 관리 앱
    - `models.py`: 도서 모델
    - `forms.py`: 도서 폼
    - `views.py`: 도서 뷰
    - `urls.py`: 도서 URL 설정
    - `admin.py`: 도서 관리 관리자 설정
    - `templates/books/`: 도서 관리 템플릿
    - `migrations/`: 마이그레이션 파일
    - `apps.py`: 앱 설정
