# 🚀 개발하기싫어요

안정적이고 확장 가능한 서버 아키텍처와 효율적인 데이터 처리를 위해 끊임없이 고민합니다. 안해요

---

### 🛠 Tech Stack

**Backend** <br>
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white) 
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white) 
![JPA](https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=flat-square&logo=spring&logoColor=white)

**Database & Cache** <br>
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white) 
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

**Infrastructure** <br>
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) 
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white) 
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=white)

---

### 🚀 Projects  임시작성용

#### **Velo (Aeranghae)** 
> AI 기반 코드 자동 생성 플랫폼

<details>
<summary><b>상세 내용 및 기술적 성취 (클릭)</b></summary>



**Architecture**
```mermaid
graph TD
    Client((사용자)) --> LB[Load Balancer]
    subgraph K8s Cluster
        LB --> Service[Service - L4]
        Service --> Pod1[Spring Boot Pod]
        Service --> Pod2[Spring Boot Pod]
    end
    Pod1 & Pod2 --> DB[(Database)]

```

**주요 기술 내용**

* **개요:** Spring Boot와 LLM을 결합한 자연어 코드 생성 서비스
* **성능 최적화:** Redis 캐싱 도입으로 DB 조회 부하 30% 감소
* **인프라:** Docker & Kubernetes를 활용한 컨테이너 기반 배포 및 자동화
* **로드밸런싱:** 쿠버네티스 Service(L4)를 통한 트래픽 분산 및 가용성 확보

**🛠 Troubleshooting**

* **문제:** 대량의 코드 생성 요청 시 DB 조회 병목 발생
* **해결:** Redis 캐싱 전략 수립 (응답속도 200ms → 50ms 단축)


* **문제:** 업데이트 시 일시적 서비스 단절
* **해결:** 쿠버네티스 Deployment 롤링 업데이트 전략 설정으로 무중단 배포 달성



---
