# MO:SI

**개인간 여행 상품 거래 플랫폼**

사용자가 직접 여행 상품을 등록하고 거래할 수 있는 플랫폼으로, 개인의 조건과 니즈에 맞는 맞춤형 여행 상품을 제공합니다.

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5-6DB33F?style=flat&logo=spring-boot&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Oracle](https://img.shields.io/badge/Oracle-21c-F80000?style=flat&logo=oracle&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-8.18-005571?style=flat&logo=elasticsearch&logoColor=white)

---

## 목차

- [시연 영상](#시연-영상)
- [프로젝트 소개](#프로젝트-소개)
- [기술 스택](#기술-스택)
- [주요 기능](#주요-기능)
- [시스템 아키텍처](#시스템-아키텍처)
- [프로젝트 구조](#프로젝트-구조)
- [팀원 및 역할](#팀원-및-역할)

---

## 시연 영상

[![MO:SI 시연 영상](https://img.youtube.com/vi/WVZkaUwPMYQ/maxresdefault.jpg)](https://www.youtube.com/watch?v=WVZkaUwPMYQ)

> 클릭하면 YouTube에서 시연 영상을 확인할 수 있습니다.

---

## 프로젝트 소개

### 배경

- 숨겨진 명소, 비인기 관광지 선호 증가 (67.2%, 한국관광공사 2024)
- 반려동물 동반 여행, 1인 여행(혼행) 트렌드 확대
- 고령층 및 취약계층 대상 맞춤형 관광 콘텐츠 부족

### 목표

1. 서비스 이용자가 자신의 조건과 니즈에 맞는 여행 상품을 찾고 구매할 수 있다.
2. 누구나 판매자가 되어 자신만의 여행 상품을 등록하고 관리할 수 있다.
3. 개인 간 거래 상품에 대한 신뢰를 구축한다.

### 개발 정보

| 항목 | 내용 |
|------|------|
| 총 개발 기간 | 2025.07.18 ~ 2025.08.29 (35일) |
| 개발 인원 | 5명 |
| 배포 환경 | 로컬 서버 |

---

## 기술 스택

### Backend
| 기술 | 버전 | 설명 |
|------|------|------|
| Spring Boot | 3.5.0 | 웹 애플리케이션 프레임워크 |
| Java | 17 | 프로그래밍 언어 |
| Spring Security | 6 | 인증/인가 |
| Spring Data JPA | 3.5 | ORM |
| Elasticsearch | 8.18.1 | 검색 엔진 |
| WebSocket (STOMP) | v13 | 실시간 통신 |

### Frontend
| 기술 | 버전 | 설명 |
|------|------|------|
| Thymeleaf | 3.1.3 | 서버 사이드 템플릿 |
| React | 19.1.1 | UI 라이브러리 |
| JavaScript | ES6 | 클라이언트 스크립트 |

### Database & Infra
| 기술 | 버전 | 설명 |
|------|------|------|
| Oracle | 21c XE | RDBMS |
| Docker | 28.0.4 | 컨테이너 |
| Git/GitHub | - | 버전 관리 |

### Tools
| 도구 | 용도 |
|------|------|
| IntelliJ IDEA | Backend 개발 |
| VS Code | Frontend 개발 |
| DBeaver | DB 관리 |
| Postman | API 테스트 |
| Figma | UI 설계 |
| Notion | 문서 관리 |

---

## 주요 기능

### 회원 관리
- 회원가입/로그인 (Spring Security)
- 판매자/구매자 역할 전환
- 회원 정보 수정

### 상품 관리
- 여행 상품 등록/수정/삭제
- 임시저장 기능
- 상품 상세 조회

### 상품 검색
- 키워드 기반 검색 (Elasticsearch)
- 자동완성
- 검색 기록 저장

### 결제 시스템
- 장바구니 담기/삭제
- 주문서 작성
- 결제 처리
- 주문/판매 내역 조회

### 리뷰 시스템
- 구매자 리뷰 작성/수정/삭제
- 판매자/구매자별 리뷰 목록 조회

### 실시간 1:1 문의
- WebSocket 기반 실시간 채팅
- 문의 내역 목록 조회

### 관광 정보 연동
- 부산 맛집 정보 (공공데이터 API)
- 교통약자 편의시설 검색

---

## 시스템 아키텍처
```
                    +------------------+
                    |      Client      |
                    | (구매자/판매자)   |
                    +--------+---------+
                             |
                    Request / Response
                             |
              +--------------+--------------+
              |           Server            |
              |  +----------------------+   |
              |  |     Spring Boot      |   |
              |  |  +---------------+   |   |
              |  |  |  Thymeleaf    |   |   |
              |  |  |  + React      |   |   |
              |  |  +---------------+   |   |
              |  |  |  WebSocket    |   |   |
              |  |  +---------------+   |   |
              |  +----------------------+   |
              +--------------+--------------+
                             |
        +--------------------+--------------------+
        |                    |                    |
   +----+----+         +-----+-----+        +-----+-----+
   |  Oracle |         |Elastic    |        |공공데이터 |
   |   DB    |         |Search     |        |   API    |
   +---------+         +-----------+        +-----------+
```

---

## 프로젝트 구조
```
src/
├── main/
│   ├── java/com/mosi/
│   │   ├── config/           # 설정 (Security, WebSocket)
│   │   ├── controller/       # API 컨트롤러
│   │   ├── service/          # 비즈니스 로직
│   │   ├── repository/       # 데이터 접근 계층
│   │   ├── domain/           # 엔티티
│   │   └── dto/              # 데이터 전송 객체
│   └── resources/
│       ├── templates/        # Thymeleaf 템플릿
│       ├── static/           # 정적 파일 (CSS, JS)
│       └── application.yml   # 설정 파일
└── test/                     # 테스트 코드
```


---

## 팀원 및 역할

| 이름 | 역할 | 담당 기능 |
|------|------|----------|
| 허진희 | 팀장 | 프로젝트 총괄, UI 구현, 실시간 채팅 |
| **김지혜** | **부팀장** | **상품 관리, 관광정보 API, 장바구니** |
| 김나리 | 팀원 | 인증/인가, 회원가입, 로그인 |
| 이현준 | 팀원 | 게시글 , 리뷰 |
| 임준영 | 팀원 | 상품 관리, 상품 목록/검색, 관광정보 API |

### 김지혜 상세 담당 업무

**개발**
- 상품 등록/수정/삭제 기능 구현
- 부산 맛집 관광정보 연동 (공공데이터 API)
- 장바구니 담기/선택삭제/전체삭제
- 주문서 작성 및 결제 처리
- 주문/판매 목록 조회

**프로젝트 관리**
- WBS 일정 관리
- 프로젝트 산출물 작성
- 통합테스트 계획 및 실행


---

## 산출물

- [포트폴리오 PDF](링크)
- [페르소나 기능정의서] (https://docs.google.com/spreadsheets/d/1QKKEvo0nVcBEJAyDEBFBM496F3-4f65r/edit?gid=1319260379#gid=1319260379)
- [요구사항 정의서](https://docs.google.com/spreadsheets/d/1VXpIZ5-rT7_fLe_U5FCXdd0h5IJrQidH/edit?gid=1561463045#gid=1561463045)
- [프로세스 설계서]([링크](https://docs.google.com/presentation/d/1_pgvyWWzQDBeBBSHaLamtox-gQQYju_f/edit?slide=id.g2dadc9c1130_1_58#slide=id.g2dadc9c1130_1_58)
- [태스크플로우](https://docs.google.com/presentation/d/1nFfK1T-nJOM0TUCwj06yfqC8fmamy5R3/edit?slide=id.p1#slide=id.p1)
- [테이블 레이아웃]((https://docs.google.com/spreadsheets/d/1ZfHPeRAbarXAKAR2D8f9YlLAZPi2QodF/edit?gid=1989820936#gid=1989820936)
- [사용자 시나리오](https://docs.google.com/presentation/d/1ZayX1U28bMgI0mGvWGw_SdUq_x-2WwSG/edit?slide=id.p1#slide=id.p1)
- [화면 설계서]([링크](https://docs.google.com/presentation/d/1K32BsfiSzPAiYfDvWd85FCkAvwKMgEiH/edit?slide=id.p1#slide=id.p1)
- [통합테스트시나리오](https://docs.google.com/spreadsheets/d/1PeNGL0axlwv94y0EeEPb_rsayCyPaZbH/edit?gid=801120606#gid=801120606)

---
