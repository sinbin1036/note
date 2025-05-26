결론부터 말하면:

> ✅ **“로그인만 성공하면” requests + BeautifulSoup 방식도 가능은 해.**  
> ❌ **하지만 실제로는 거의 대부분 실패하거나 매우 불안정해.**

아래에서 이유 딱 정리해줄게.

---

## 🧪 네가 말한 방식: 로그인 후 requests로 긁기

|순서|설명|
|:--|:--|
|1|`requests.Session()`으로 로그인 요청 보내기 (`POST /login` 등)|
|2|쿠키/세션 저장|
|3|로그인된 상태 유지하면서 `GET /course/list` 같은 URL 접근|
|4|HTML 받아서 `BeautifulSoup`으로 파싱|

---

## ❗ 그런데 왜 실패할 가능성이 크냐면?

### 1. ❌ **로그인 API 요청이 명확하지 않음**

- 수강신청 사이트가 iframe + JavaScript 기반일 가능성이 높음
    
- 개발자도구(F12) 열어도 `POST /login` 같은 요청 안 보였을 가능성 크지?
    
- 이건 **폼 기반 로그인**이 아니라 **JavaScript 내부 처리**라 requests로 복제 어려움
    

---

### 2. ❌ **세션 유지 실패**

- 서버가 로그인 후 `Set-Cookie`, `CSRF Token` 같은 보안 헤더를 요구하는 경우 많음
    
- requests만으로 그걸 흉내내는 건 복잡하고, 안 되면 바로 로그인 실패
    

---

### 3. ❌ **콘텐츠가 JavaScript로 렌더링됨**

- 로그인 후 강의 리스트가 `HTML` 안에 바로 안 들어 있음
    
- 페이지가 열릴 때 JS가 서버로 비동기 요청 → HTML 안에 아무것도 없음
    
- `requests.get()` 하면 빈 div만 날아올 수 있음
    

---

## ✅ 그래서 Selenium이 필요한 이유

|기능|requests|Selenium|
|:--|:--|:--|
|실제 브라우저 실행|❌|✅|
|JavaScript 렌더링|❌|✅|
|사람처럼 로그인|❌ (API 필요)|✅ (입력창에 send_keys 가능)|
|동적 페이지 처리|❌|✅|
|학교 수강신청 사이트에 적합|❌|✅|

---

## ✅ 결론

> **“수강신청 사이트가 로그인 요청을 단순 POST로 처리하고,  
> 로그인 후 HTML 안에 바로 과목 정보가 있다면 가능하다.  
> → 하지만 실제로는 거의 대부분 안 된다.”**

그래서 **Selenium이 사실상 유일한 방법**이라고 했던 거야.

---

원하면 한 번 실제로 `requests.Session()` 방식으로 시도해볼 수는 있어.  
👉 “로그인 세션 방식으로 시도해보자”라고 하면 예제 코드도 짜줄게.  
하지만 확률 낮다는 것만 감안하고 도전하는 게 좋아.

할래? 아니면 바로 Selenium으로 가자. 🔥

출처 기술 :  https://96-brain.tistory.com/79


크롤링이 보안적문제가 있을꺼 같은데 DB, FASTAPI를 이용해서
백엔드로 데이터를 올린다면 크롤링자체 소스파일은 올라가지 않아
보안을 확보 할수 잇는가?

# 📘 DCP - DSU Course Plus

---

## 🛬 프로젝트 개요

> 기존 수강시청 시스템에는 수업을 요일별, 시간별로 **빠른 것을 찾는 기능이 없다.**  
> `DCP`는 **대학생이 원하는 시간대의 수업을 빠른 것으로 찾을 수 있도록 도움을 주는 보조 앱**이다.

---

## 🌟 주요 기능

- 요일 / 규식 / 전공 / 교양 필터 기능 제공
- 과념명, 교수명으로 검색 가능 (추가 예정)
- **모든 수업 데이터는 관리자 1인이 학교 수강시청 사이트에서 수정**
- 사용자 로그인 없이 누구나 앱에서 필터 기능 사용 가능

---

## 🧱 시스템 구성 요약

```
[관리자 1인]
    → Selenium으로 로그인 후 수업 전체 크롤링
    → 크롤링 결과를 DB(MySQL)에 저장

[FastAPI 서버]
    → /subjects API로 필터링된 수업 목록 제공 (day, time, type 등)

[Android 앱]
    → 서버 API를 호출해서 사용자에게 수업 필터 결과 표시
```

---

## 🔐 보안 정책

- 사용자는 도서대학교 계정으로 로그인할 필요 없음
- 서버는 크롤링을 복소하지 않음 → **학교 서버에 보도를 준 적 없음**
- 모든 수업 데이터는 수단 수정 → 안정적, 예측 가능

---

## ⚙️ 기술 스테크

| 영역 | 기술 |
|:--|:--|
| 백어드 | Python + FastAPI |
| DB | MySQL + SQLAlchemy |
| 크롤링 | Selenium (ChromeDriver) |
| 앱 | Android Studio (Java or Kotlin), Retrofit |
| API 테스트 | Swagger UI (FastAPI 내장) or Postman |

---

## SETUP

### 1. 파이썬 설치
https://www.python.org/downloads/

```
python --version
```

```
pip --version
```
제대로 설치되었는지 확인


### 2. vscode 필수 확장

#### ✅ FastAPI + Python 개발용 필수 확장
Python

⛳ 가장 기본. Linting, Debugging, 가상환경, 실행 다 됨

개발자: Microsoft

#### Pylance

🧠 자동완성 + 타입 추론 + IntelliSense 강화

꼭 Python 확장과 함께 써야 함

#### Jinja

만약 FastAPI에서 HTML 템플릿 쓸 생각 있다면 (Jinja2 지원)

#### REST Client

💡 FastAPI 테스트할 때, HTTP 요청을 .http 파일에서 바로 보낼 수 있음 (Postman 대체)

SQLite Viewer / SQLite

📊 .db 파일 직접 보고, 쿼리 날릴 수 있음

### chromedriver

https://storage.googleapis.com/chrome-for-testing-public/136.0.7103.94/win64/chromedriver-win64.zip

### 3. install module

```
pip install selenium
```

---

## 🤩 주요 API 명세

```
GET /subjects?day=화&time=3&type=전공
```

**응답 예시:**

```json
[
  {
    "dept": 소프트웨어학과,
    "grade": 3학년,
    "class_id": 123456,
    "class_num": 101,
    "class_name": 소프트웨어개발실습3,
    "professor": 김동현,
    "credit": 3,
    "schedule": {day: 화 ,time: 1-2},
    "type": 전공필수,
    "general_area": UIT관,
    "lecture_area": null 
  }
]
```

---

## 🚀 운영 화면 요약

| 단계 | 설명 |
|:--|:--|
| 1 | **관리자가 수강시청 사이트에 로그인 → 수업 목록 크롤링** |
| 2 | **크롤링 결과를 MySQL DB에 저장** |
| 3 | FastAPI 서버가 DB를 조회해서 API로 사용자에게 응답 |
| 4 | Android 앱에서 API를 호출해서 사용자에게 수업 필터 결과 표시 |

---

## 📅 개발 일정 (uc608시)

| 주차 | 목표 |
|:--|:--|
| 1주차 | 크롤링 구현 및 수업 데이터 샘플 확률 |
| 2주차 | MySQL DB 설계 및 연동 |
| 3주차 | FastAPI API 완성 및 테스트 |
| 4주차 | Android 앱 UI + API 연동 |
| 5주차 | 통합 테스트 / 발표 준비 |

---

## 🧠 마무리 요약

> **"우리는 학교 수강시청 시스템에 부담을 주지 않으며,  
> 사용자가 수업을 효율적으로 찾을 수 있도록 도움을 주는 앱을 만듭니다."**  
> 관리자 단일 계정으로 1회만 크롤링해서 효율성과 안정성 모두 확답합니다
