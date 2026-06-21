<!-- ╔══════════════════════════════════════════════════════════╗ -->
<!-- ║  HEADER                                                    ║ -->
<!-- ╚══════════════════════════════════════════════════════════╝ -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A0E13,100:F2A24C&height=200&section=header&text=Chanho%20Kim&fontSize=52&fontColor=ffffff&fontAlignY=38&desc=Backend%20Developer%20|%20Platform%20Builder%20|%20AI-Driven%20Engineering&descSize=16&descAlignY=60" width="100%" />

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=22&duration=3500&pause=900&color=F2A24C&center=true&vCenter=true&width=720&lines=Don%27t+build+services+repeatedly.;Build+a+platform+that+builds+services.)](https://github.com/Chanho-Kim)

</div>

> ### "Don't build services repeatedly. Build a platform that builds services."

현재 AI 기반 개발 환경(**Claude Code · Harness · Superpowers**)을 활용해 개발 생산성을 극대화하는 방법을 연구하고 있습니다.
코드 작성은 더 이상 병목이 아닙니다 — 진짜 병목은 **인프라 · 아키텍처 설계 · 서비스 간 연동**입니다.
그래서 새 프로젝트마다 반복되는 작업을 제거하기 위해 재사용 가능한 **MSA Starter Platform** 을 구축하고 있습니다.

<br/>

### 🛠️ Tech Stack

<div align="center">

![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Java](https://img.shields.io/badge/Java-437291?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Cloud Gateway](https://img.shields.io/badge/Spring_Cloud_Gateway-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Keycloak](https://img.shields.io/badge/Keycloak-4D4D4D?style=for-the-badge&logo=keycloak&logoColor=white)
<br/>
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-FF4438?style=for-the-badge&logo=redis&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Vault](https://img.shields.io/badge/HashiCorp_Vault-FFEC6E?style=for-the-badge&logo=vault&logoColor=black)
<br/>
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![ArgoCD](https://img.shields.io/badge/Argo_CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
<br/>
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white)

</div>

---

## 🎯 목표

- **빠른 프로젝트 시작** — 표준화된 환경으로 보일러플레이트 최소화
- **MSA Best Practice** 기본 적용
- **확장 가능한 아키텍처** — 서비스 / 인프라 교체 및 추가 용이
- **CI/CD 및 모니터링** 기본 제공
- **단계적 성장** — 1단계 (Compose) → 2단계 (K8s) → 3단계 (AI)

---

<!-- ╔══════════════════════════════════════════════════════════╗ -->
<!-- ║  MSA STARTER TEMPLATE                                       ║ -->
<!-- ╚══════════════════════════════════════════════════════════╝ -->

## 🏗️ MSA Starter Template

> 확장 가능한 MSA(Microservice Architecture) 개발 기본 템플릿
> **단계별 학습 목표 프로젝트** — Docker Compose → Kubernetes + ArgoCD → Spring AI

표준화된 환경에서 빠르게 시작하고, 공통 모듈을 재사용하며, 인프라를 자유롭게 교체·확장할 수 있는 MSA 스타터 템플릿입니다.
로컬 개발(Docker Compose)부터 운영 배포(Kubernetes), AI 기능 확장까지 단계적으로 성장하도록 설계했습니다.

<div align="center">
  <img width="900" alt="MSA Starter Template Architecture with Vault" src="https://github.com/user-attachments/assets/55fcc063-e024-4295-bad6-c3c529622bd5" />
</div>

---

## 🔀 아키텍처 개요

```mermaid
flowchart LR
    Client["Client<br/>(Web / Mobile)"] --> Nginx["Nginx<br/>Reverse Proxy · SSL"]
    Nginx --> Gateway["API Gateway<br/>Spring Cloud Gateway"]
    Gateway --> Services["MSA Services<br/>(Spring Boot)"]
    Keycloak["Keycloak<br/>OAuth2 / OIDC / JWT"] -.JWT 검증.-> Gateway
    Services --> Infra["Infrastructure Layer<br/>MySQL · Redis · Kafka · Vault"]
    Services --> Observe["Observability<br/>Prometheus · Grafana"]
```

요청 흐름: **Client → Nginx → API Gateway → MSA Services**
인증은 **Keycloak** 이 담당하고, Gateway 단에서 JWT를 검증합니다.

---

## 🧩 핵심 구성 요소

### Gateway & 인증
| 구성 | 역할 |
|------|------|
| **Nginx** | Reverse Proxy, Static Files, SSL Termination |
| **API Gateway** (Spring Cloud Gateway) | Routing, Filter, Rate Limiting, Circuit Breaker, Logging |
| **Keycloak** | OAuth2 / OIDC, SSO, JWT, RBAC |

### 공통 모듈 (Common Modules)
| 모듈 | 역할 |
|------|------|
| `starter-core` | 공통 핵심 기능 |
| `starter-security` | 보안 / 인증 / 인가 |
| `starter-logging` | 로그 / MDC / 추적 |
| `starter-domain` | 공통 도메인 / 유틸 |

### 인프라 (Infrastructure Layer)
| 구분 | 구성 | 역할 |
|------|------|------|
| **Data** | MySQL | 관계형 데이터 |
| **Data** | Redis | Cache / Session |
| **Data** | Kafka `선택` | 이벤트 스트리밍 |
| **Data** | OpenSearch `선택` | 검색 / 분석 |
| **Secret** | HashiCorp Vault | DB Password · API Keys · JWT Secret · 외부 서비스 키 관리 |

<details>
<summary><b>Cross-Cutting Infra (2차 이후)</b></summary>

| 구성 | 역할 |
|------|------|
| Config Server | 설정 중앙화 |
| Service Discovery | Eureka / Consul |
| Vault | Secret 관리 |
| OpenTelemetry | 분산 추적 |
| Loki | 로그 수집 |
| Istio `선택` | Service Mesh |

</details>

### 관측 & 모니터링 (Observability)
| 구성 | 역할 |
|------|------|
| **Spring Actuator** | 애플리케이션 모니터링 |
| **Prometheus** | Metrics 수집 |
| **Grafana** | 시각화 / 대시보드 |
| **Alertmanager** | 알림 |

---

## 🔧 DevOps & CI/CD Pipeline

```mermaid
flowchart LR
    A["GitHub<br/>소스"] --> B["Jenkins<br/>빌드/테스트"]
    B --> C["SonarQube<br/>코드 품질"]
    C --> D["Nexus<br/>아티팩트"]
    D --> E["Docker Build<br/>이미지 빌드"]
    E --> F["Registry<br/>Push"]
```

---

## 🚀 단계별 로드맵

#### Phase 1 — Docker Compose 기반 개발환경 ✅
- [x] 핵심 인프라 제공 · 빠른 로컬 개발 환경
- [x] 일관된 개발 경험
- [x] `docker compose up -d` 로 전체 환경 실행

#### Phase 1.5 — 메시징 / 검색 기능 확장 `선택`
- [ ] **Kafka** — 이벤트 처리(비동기)
- [ ] **OpenSearch** — 검색 / 로그 분석

#### Phase 2 — Kubernetes + ArgoCD 배포
- [ ] 컨테이너 오케스트레이션
- [ ] GitOps 기반 배포
- [ ] 확장성 / 고가용성

#### Phase 3 — Spring AI 추가
- [ ] AI Gateway · LLM 연동 (OpenAI, Claude 등)
- [ ] 문서 요약 / 생성
- [ ] 자동화 / 챗봇 등

---

## 📦 배포 환경

| 단계 | 환경 | 구성 |
|------|------|------|
| **1차** | Docker Compose (개발) | Nginx · Gateway · Keycloak · MSA Services · MySQL · Redis · Kafka · OpenSearch · Prometheus · Grafana |
| **2차** | Kubernetes + ArgoCD (운영) | K8s 오케스트레이션 + ArgoCD GitOps 배포 |

---

## ➕ 새 서비스 추가 방법

1. `starter-template` 기반 새 서비스 생성
2. 공통 모듈 의존성 추가
3. `application.yml` / Config 설정
4. Gateway 라우팅 등록
5. 배포 (Compose / K8s)

---

## 📚 학습 포인트

- MSA 기본 구조와 서비스 간 통신
- API Gateway / 인증·인가 (Keycloak, JWT)
- 공통 모듈 설계와 재사용
- 인프라 구성 (DB · 캐시 · 메시징 · 시크릿 관리)
- 관측성(Observability) 및 모니터링 체계
- CI/CD 파이프라인 구축
- 컨테이너 오케스트레이션과 GitOps (K8s · ArgoCD)
- AI 기능 통합 (Spring AI)

> 🗂️ **로드맵 & 공부 정리** — [학습 공간](https://app.notion.com/p/9feba17c225e4cfc9ca149c15c9a3443) · [공부 로드맵](https://app.notion.com/p/380a0d2516be80d49931e9aa35de19ac)

---

<!-- ╔══════════════════════════════════════════════════════════╗ -->
<!-- ║  GITHUB STATS  ─  아래 YOUR_GITHUB_ID 를 본인 깃허브 아이디로 ║ -->
<!-- ╚══════════════════════════════════════════════════════════╝ -->

<div align="center">

![Stats](https://github-readme-stats.vercel.app/api?username=chanho4702&show_icons=true&hide_border=true&title_color=F2A24C&icon_color=F2A24C&text_color=8B98A7&bg_color=0A0E13)
![Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=chanho4702&layout=compact&hide_border=true&title_color=F2A24C&text_color=8B98A7&bg_color=0A0E13)

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:F2A24C,100:0A0E13&height=120&section=footer" width="100%" />
