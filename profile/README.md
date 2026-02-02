<div align="center">

# 🎫 NextFrame
### 대규모 트래픽을 감당할 수 있는 견고한 티켓팅 서비스

<br/>

[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![Java](https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://docs.oracle.com/en/java/javase/21/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)

<br/>

> **"수만 명의 동시 접속에도 멈추지 않는 안정성"**
>
> **NextFrame**은 공연 일정 조회부터 좌석 선택, 결제, 그리고 QR 티켓 발급까지<br>
> 끊김 없는 사용자 경험을 제공하는 예매 플랫폼입니다.

</div>

<br/>

---

## 📝 Table of Contents

1. [Links](#-links)
2. [Project Overview](#-project-overview)
3. [Key Features](#-key-features)
4. [Tech Stack](#-tech-stack)
5. [System Architecture & ERD](#-system-architecture--erd)
6. [Team Members](#-team-members)
7. [Collaboration Rules](#-collaboration-rules-ground-rules)

<br/>

---

## 🔗 Links
- **Service URL:** [https://nextframe.wisoft.dev/](https://nextframe.wisoft.dev/)
- **API Documentation:** [Swagger UI Docs](https://next-frame-lab.github.io/swagger-ui-docs/)

<br/>

---

## 📅 Project Overview

### 🚩 Background

<table>
<tr>
<td width="50%" align="center" valign="middle">
<h3>"서버가 터졌어요"</h3>
<p>유명 아이돌 콘서트 티켓팅 시<br>빈번하게 발생하는 <b>서버 다운</b> 현상</p>
</td>
<td width="50%" align="center" valign="middle">
<h3>"제 자리가 없어졌어요"</h3>
<p>동시 접속자로 인한 <b>이중 예매(Race Condition)</b><br>및 데이터 정합성 문제</p>
</td>
</tr>
</table>

<br/>

### 💎 Core Values

**NextFrame**은 단순한 예매 기능을 넘어, 극한의 트래픽 상황에서도 신뢰할 수 있는 시스템을 구축했습니다.

<table>
<tr>
<td width="33%" align="center" valign="middle">
<h3>견고함 (Stability)</h3>
<p>분산 락(Distributed Lock)을 통해<br/>단 하나의 좌석도 중복되지 않도록<br/><b>데이터 정합성</b>을 보장합니다.</p>
</td>
<td width="33%" align="center" valign="middle">
<h3>성능 (Performance)</h3>
<p>Redis 캐싱과 대기열 시스템으로<br/><b>대규모 트래픽</b>을 효율적으로<br/>처리하고 부하를 분산합니다.</p>
</td>
<td width="33%" align="center" valign="middle">
<h3>경험 (Experience)</h3>
<p>직관적인 UI와 반응형 디자인으로<br/>사용자에게 <b>끊김 없는<br/>예매 경험</b>을 제공합니다.</p>
</td>
</tr>
</table>

<br/>

---

## ✨ Key Features

| 기능 | 상세 설명 |
|:---:|:---|
| **🔐 인증/인가** | • OAuth 2.0 (카카오 등) 소셜 로그인<br>• JWT 기반의 보안성 높은 세션 관리 |
| **🎫 공연 예매** | • 공연 검색 및 상세 정보 조회 (캐싱 적용)<br>• 실시간 좌석 상태 확인 및 선점 (Concurrency Control) |
| **💳 결제 시스템** | • 결제 검증 및 보안 처리<br>• 결제 실패 시 트랜잭션 롤백 및 좌석 점유 해제 |
| **📱 티켓 관리** | • 예매 내역 확인 및 QR 코드 티켓 발급<br>• 사용자 리뷰 및 평점(좋아요) 시스템 |

<br/>

---

## 🛠 Tech Stack

### Frontend
* **Language:** TypeScript 5.8.3
* **Framework:** React 18.3.1
* **Styling:** TailwindCSS
* **State Management:** Recoil
* **Server State Management:** TanStack Query
* **Test:** Jest, React Testing Library

### Backend
* **Language:** Java 21
* **Framework:** Spring Boot 3.5.4
* **Test:** JUnit5, Mockito
* **ORM:** JPA, QueryDSL

### Database
* **RDBMS:** PostgreSQL
* **NoSQL:** Redis

### Infrastructure & Deployment
* **Server:** On-Premise
* **Virtualization:** Docker
* **CI/CD:** GitHub Actions
* **Web Server(Reverse Proxy):** Nginx

<br/>

---

## 📐 System Architecture & ERD
> 현재 아키텍처와 DB 설계도는 지속적으로 고도화 중입니다.

### System Architecture
<details>
<summary><b>👉 시스템 아키텍처 구성도 펼쳐보기</b></summary>
<br>

![System Architecture](../images/service_architecture.png)

</details>

<br>

1. **서비스 독립 분리 및 API 라우팅**
   - Payment, Schedule-Reservation-Ticketing, Payment-Gateway 애플리케이션 독립 운영
   - Nginx Reverse Proxy: React 정적 리소스 및 백엔드 API 단일 진입점(Single Entry Point) 구성
   - 통신 프로토콜: 서비스 간 REST API 표준 인터페이스 적용

2. **CI/CD**
   - 조건부 빌드: changed-files 액션을 통한 변경 모듈 감지 및 선별적 빌드/배포
   - Bastion 터널링: 내부망 환경 보안을 위한 SSH 터널링 기반 아티팩트(.jar) 전송

3. **Database**
   - 분산 락(Redisson): Redis 기반 락 구현으로 좌석 예매 시 발생하는 Race Condition 방지
   - 데이터 캐싱: 조회 빈도가 높은 공연 정보 Redis 캐싱을 통한 DB 부하 감소 및 응답 속도 개선
   - 데이터 통합 관리: PostgreSQL 통합 DB 구성을 통한 분산 환경 내 데이터 정합성 유지

4. **보안 및 모니터링**
   - 네트워크 격리: Bastion Server를 경유한 SSH 접근 제어 (내부망 격리)
   - 인증/인가: OAuth 2.0 기반 소셜 로그인 및 JWT 토큰 검증
   - 가시성 확보: Prometheus/Grafana/Loki 스택을 활용한 메트릭(CPU, Memory) 및 API 처리 현황 실시간 모니터링

<br>

### ERD (Entity Relationship Diagram)
<details>
<summary><b>👉 ERD (DB 설계도) 펼쳐보기</b></summary>
<br>

![NextFrame ERD](../images/DB_diagram.png)

</details>

<br>

---

## 👥 Team Members

### 🦌 Backend Team
<table align="center">
    <tr>
        <td align="center" width="250" valign="top">
            <img src="https://github.com/git-mesome.png" width="120" height="120" style="border-radius: 50%;"/><br/>
            <b>김민서</b><br/>
            <sub>Team Leader / Backend</sub><br/>
            <a href="https://github.com/git-mesome">
                <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white"/>
            </a>
        </td>
        <td width="500" valign="middle">
            <ul>
                <li><b>좌석 결제 및 환불 프로세스 구현</b></li>
                <li>티켓(QR 코드) 발급 시스템</li>
                <li>공연 검색 기능 고도화 (QueryDSL)</li>
                <li>DB/배포/모니터링 환경 구축 및 DB 설계</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td align="center" width="250" valign="top">
            <img src="https://github.com/Jinpyo-An.png" width="120" height="120" style="border-radius: 50%;"/><br/>
            <b>안진표</b><br/>
            <sub>Backend Developer</sub><br/>
            <a href="https://github.com/Jinpyo-An">
                <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white"/>
            </a>
        </td>
        <td width="500" valign="middle">
            <ul>
                <li><b>공연 좌석 및 예매 프로세스 구현</b></li>
                <li>소셜 로그인(OAuth2) 및 JWT 인증/인가</li>
                <li>공연 검색 및 리뷰(좋아요) 기능</li>
                <li>배포 환경 구축 및 API 설계</li>
            </ul>
        </td>
    </tr>
</table>

<br>

### 🎨 Frontend Team
<table align="center">
    <tr>
        <td align="center" width="250" valign="top">
            <img src="https://github.com/Geunone2.png" width="120" height="120" style="border-radius: 50%;"/><br/>
            <b>박근원</b><br/>
            <sub>Frontend Developer</sub><br/>
            <a href="https://github.com/Geunone2">
                <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white"/>
            </a>
        </td>
        <td width="500" valign="middle">
            <ul>
                <li>GitHub Actions CI/CD 구축</li>
                <li>결제, 공연, 좌석 등 핵심 도메인 기능 구현</li>
                <li>결제, 공연, 좌석 등 핵심 도메인 기능 단위 테스트 진행</li>
                <li>OAuth Bearer 토큰 인증을 통한 페이지 접근 제한 & 승인 구현</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td align="center" width="250" valign="top">
            <img src="https://github.com/kaeuhy.png" width="120" height="120" style="border-radius: 50%;"/><br/>
            <b>강은현</b><br/>
            <sub>Frontend Developer</sub><br/>
            <a href="https://github.com/kaeuhy">
                <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white"/>
            </a>
        </td>
        <td width="500" valign="middle">
            <ul>
                <li>정적 페이지 및 반응형 CSS 구현</li>
                <li>메인 페이지 공연 목록 API 연동</li>
                <li>카카오 로그인/회원가입 OAuth 구현</li>
                <li>Recoil 상태 관리를 통한 토큰 관리</li>
            </ul>
        </td>
    </tr>
</table>

<br>

---

## 🤝 Collaboration Rules (Ground Rules)
NextFrame 팀은 명확한 규칙을 통해 코드 품질을 유지하고 협업 효율을 높입니다.

### 1. Git Strategy
* **Git Flow** 전략을 따릅니다. (`main`, `develop`, `feature`, `release`, `hotfix`)
* **Merge Strategy:** `Rebase and Merge`를 사용하여 커밋 히스토리를 깔끔하게 관리합니다.

### 2. Code Convention
* [Naver Java Coding Convention](https://naver.github.io/hackday-conventions-java/)을 준수합니다.

### 3. Commit Message Convention
이슈 트래킹을 위해 아래 템플릿을 엄격히 준수합니다.

```text
#<이슈번호> <타입>(<범위>): <제목> (제목은 40자 이내)

<본문> (선택 사항, 한 줄 띄우고 작성. 72자 이내로 줄 바꿈)

Resolves: #<이슈번호>
See also: None (관련 항목이 있으면 #<이슈번호> 기입)
```

</br>

<div align="center"> Made with ❤️ by <b>NextFrame Team</b> </div>