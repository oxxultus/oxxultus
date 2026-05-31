# 개발하기싫어요

안정적이고 확장 가능한 서버 아키텍처와 효율적인 데이터 처리를 위해 끊임없이 고민합니다. 안해요

---

<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; font-size: 12px; font-weight: bold;">Backend</span><br>
![Java](https://img.shields.io/badge/JAVA-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/SPRING%20BOOT-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Web MVC](https://img.shields.io/badge/SPRING%20WEB%20MVC-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/SPRING%20DATA%20JPA-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Data Redis](https://img.shields.io/badge/SPRING%20DATA%20REDIS-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Security](https://img.shields.io/badge/SPRING%20SECURITY-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
<br>

<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; font-size: 12px; font-weight: bold;">Database & Cache</span><br>
![Oracle](https://img.shields.io/badge/ORACLE-F80000?style=flat-square&logo=oracle&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/POSTGRESQL-316192?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MYSQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/REDIS-DC382D?style=flat-square&logo=redis&logoColor=white)
<br>

<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; font-size: 12px; font-weight: bold;">Infrastructure</span><br>
![Nginx](https://img.shields.io/badge/NGINX-009639?style=flat-square&logo=nginx&logoColor=white)
![Kubernetes](https://img.shields.io/badge/KUBERNETES-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/DOCKER-2496ED?style=flat-square&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/LINUX-FCC624?style=flat-square&logo=linux&logoColor=white)

---

### Projects  임시작성용

#### **[Velo (Team: Aeranghae)](https://github.com/aeranghae/velo-main-api)** 
> AI 기반 코드 자동 생성 플랫폼

<details>
<summary><b>상세 내용 및 기술적 성취 (클릭)</b></summary>


**Architecture**
![Velo System Architecture](images/velo-system-architecture.gif)

**주요 기술 내용**

* **개요:** Spring Boot와 LLM을 결합한 자연어 코드 생성 서비스
* **성능 최적화:** Redis 캐싱 도입으로 DB 조회 부하 30% 감소
* **인프라:** Docker & Kubernetes를 활용한 컨테이너 기반 배포 및 자동화
* **로드밸런싱:** 쿠버네티스 Service(L4)를 통한 트래픽 분산 및 가용성 확보

<details>
<summary><b>Troubleshooting (기술적 문제 해결 및 아키텍처 고민) 이후3개만 남기고 다뺄거임</b></summary>

#### 1. [Resource] 물리 경로와 논리 이름 분리를 통한 디렉토리 충돌 방지
- **문제 상황:** 사용자 설정 이름으로 스토리지 폴더 생성 시, 프로젝트명 변경에 따른 디스크 I/O 병목 및 동일 이름 프로젝트 간의 폴더 충돌 위협 발견.
- **해결책:** 물리 디렉토리는 고유 식별자(`UUID`)로 완전히 격리하고, 화면 표시용 이름은 DB 메타데이터로 매핑하는 구조적 분리(Decoupling)를 통해 물리-논리 아키텍처 무결성 확보.
- **결과:** 사용자가 프로젝트 이름을 자유롭게 변경하더라도 실제 파일 시스템의 경로가 깨지거나 파일이 유실되는 위험을 원천 차단함.

#### 2. [Security] 인프라 자원 보호를 위한 스토리지 할당 시점 제어 
- **문제 상황:** 회원가입 절차를 마치지 않은 가상 사용자의 무분별한 유입 시 스토리지 공간이 무한 생성되어 서버 디스크 고갈(DoS) 위협 발생.
- **원인 분석:** OAuth 인증 직후 가입을 완료하지 않은 익명(`GUEST`) 유저에게까지 물리 스토리지를 무조건 할당하는 느슨한 자원 정책이 원인이었음.
- **해결책:** `if (user.getRole() == Role.USER)` 가드 조건을 비비즈니스 레이어에 매핑하여, 정식 유저 승급 시점에만 격리 샌드박스 공간을 할당하도록 자원 관리 정책 정교화.
- **결과:** 유령 폴더 생성을 막아 서버 리소스 낭비를 방지하고 악의적인 자원 고갈 공격 방어선을 구축함.

#### 3. [I/O Optimization] Files.walk 전수 스캔 병목 개선을 위한 메타데이터 캐싱 전략 ✓
- **현상 (Problem):** 사용자가 저장소 내 프로젝트의 파일 트리와 실시간 용량을 조회할 때마다 API 응답 속도가 점진적으로 저하되는 성능 저하 우려 발견.
- **원인 (Cause):** 사용자 요청이 들어올 때마다 자바의 `Files.walk` API를 사용해 파일 시스템(NFS)의 실제 물리 디렉토리를 바닥부터 끝까지 전수 스캔하도록 설계되어 있었습니다. 프로젝트 내 파일 개수와 볼륨이 늘어날수록 디스크 I/O 병목이 심해져 서버 전체의 쓰루풋(Throughput)을 떨어트리는 구조적 결함이 있었습니다.
- **해결 (Action):** 조회 시마다 디스크를 긁어오던 무거운 동기화 방식을 전면 폐기했습니다. 대신 AI 자율 코딩 공정이 최종적으로 완수(`COMPLETED` 또는 `FAILED`)되는 시점에 단 한 번 파일 트리와 용량을 일괄 색인(`indexProjectFiles`)하여 DB(PostgreSQL JSONB 컬럼)에 장부 형태로 기록하도록 아키텍처를 변경했습니다.
- **결과 (Result):** 물리 디스크 접근 횟수를 0번으로 줄이고, 사용자 조회 요청 시 JPA 영속성 레이어 및 Redis 캐시 레이어에서 메타데이터를 **0.0001초 만에 즉시 서빙**하도록 성능을 극대화했습니다. 무조건적인 실시간 조회보다 시스템 부하를 고려한 '장부 기반 색인 및 캐싱 아키텍처'의 필요성을 학습했습니다.

#### 4. [Data Integrity] 재귀적 디렉토리 파괴 알고리즘 구축
- **문제 상황:** 자바 표준 `Files.delete()`의 특성상 비어있지 않은 폴더 삭제가 불가능하여, 프로젝트 삭제 시 디스크에 찌꺼기 파일이 남는 데이터 불일치 현상 발생.
- **해결책:** 하위 데이터 노드부터 역순으로 탐색하여 리프 파일들을 선제 제거하는 `deleteDirectoryRecursive` 재귀 알고리즘을 구현하여 물리-논리 데이터 정합성 100% 일치 도달.
- **결과:** 프로젝트 삭제 요청 시 데이터베이스 장부와 물리 저장소 폴더가 완전히 일괄 소멸되는 정합성을 보장함.

#### 5. [Network/Security] Spring Security와 CORS Preflight 필터 순서 오설정 해결 ✓
- **현상 (Problem):** 프론트엔드(React) 클라이언트에서 PATCH, DELETE 등 특정 HTTP 메서드로 요청을 보낼 때, 인가 실패(`403 Invalid CORS request`) 에러가 연쇄적으로 격발됨.
- **원인 (Cause):** 브라우저가 안전한 통신을 위해 선제적으로 전송하는 `OPTIONS (Preflight)` 요청은 인증 토큰을 지니지 않는다는 특징이 있습니다. 하지만 기존 아키텍처에서는 토큰을 검증하는 `JwtAuthenticationFilter`가 CORS 가드 역할을 하는 `CorsFilter`보다 앞단에 배치되어 있었습니다. 이로 인해 토큰이 없는 Preflight 요청이 CORS 검증을 받기도 전에 시큐리티 가드에 막혀 응답 헤더를 정상적으로 발급받지 못한 것이 원인이었습니다.
- **해결 (Action):** `addFilterBefore` 설정을 교정하여 `JwtAuthenticationFilter`의 진입 포지션을 `CorsFilter` 뒷단(UsernamePasswordAuthenticationFilter 앞)으로 재배치했습니다. 토큰이 없는 Preflight 요청이 CORS 승인 헤더를 먼저 안전하게 발급받아 통과할 수 있도록 필터 파이프라인 구조를 수정했습니다.
- **결과 (Result):** 복잡한 HTTP 메서드 요청 시 발생하던 CORS 거부 문제를 완벽히 해결하여 프론트-백엔드 간의 안정적인 보안 통신 인프라를 확보했습니다. 웹 보안 표준과 스프링 시큐리티 필터 체인의 생명주기를 깊이 이해하는 계기가 되었습니다.

#### 6. [Data] Spring Data Redis 4.0 직렬화 빌더 패턴 대응 및 예외 방어
- **문제 상황:** Spring Data Redis 4.0 업그레이드에 따라 기존 구버전 기반의 `GenericJackson2JsonRedisSerializer` 및 `create()` 팩토리 메서드가 Deprecated되어 컴파일 예외 발생.
- **해결책:** 최신 가이드라인에 맞춰 `GenericJacksonJsonRedisSerializer.builder()` 패턴으로 전면 리팩토링을 단행하고, 객체 다형성 보장 시 발생할 수 있는 역직렬화 `ClassCastException`을 방어하기 위해 `BasicPolymorphicTypeValidator`를 통한 최상위 `Object.class` 타입 바인딩 커스텀 설정 완료.
- **결과:** 최신 릴리스 명세에 맞춘 안전한 인메모리 데이터 직렬화 환경을 구성하고 중복 생성되던 Serializer 객체를 빈으로 관리하여 재사용성을 높임.

#### 7. [Performance] 웹소켓 세션 타임아웃 및 대용량 로그 스트리밍 버퍼 초과 현상 최적화 ✓
- **현상 (Problem):** AI 에이전트가 격리 샌드박스 내부에서 코드를 생성하고 Gradle 빌드 및 쉘 명령어를 실행하는 과정에서, 실시간 로그 스트리밍 도중 웹소켓 연결이 중간에 끊기거나 특정 대용량 로그 구간에서 데이터가 잘리는 현상이 발생함.
- **원인 (Cause):** 스프링 웹소켓의 기본 세션 유지 타임아웃(Idle Timeout) 설정이 너무 짧아, AI 엔진의 빌드 연산이 길어질 때 무동작 상태로 오인되어 커넥션이 강제 종료되었습니다. 또한, Gradle 빌드 시 쏟아져 나오는 방대한 표준 출력(`stdout`) 로그의 데이터 체급이 스프링 웹소켓 컨테이너의 기본 텍스트 버퍼 임계치를 초과하여 세션 오버플로우 예외가 격발된 것이 원인이었습니다.
- **해결 (Action):** `ServletServerContainerFactoryBean` 설정을 커스텀 정의하여 스프링 웹소켓의 인프라 한계를 직접 확장했습니다. AI 장기 연산 환경을 고려해 세션 및 비동기 송신 타임아웃을 **5분(300,000ms)**으로 상향 조정하고, 대용량 로그 수신 시 데이터 유실을 막기 위해 텍스트 및 바이너리 메시지 버퍼 크기를 **10MB**로 대폭 확충했습니다.
- **결과 (Result):** 네트워크 병목이나 인프라 제약 없이 AI 자율 공정 전체 프로세스의 대용량 빌드 로그를 100% 무결하게 실시간으로 스트리밍하는 데 성공했습니다. 네트워크 세션 관리와 메모리 버퍼 임계치 설계의 중요성을 깨달았습니다.

---

</details>
</details>


#### **[Liminal (Side)](https://github.com/oxxultus/liminal)** 
> 다중 LLM 엔진과 MCP 플러그인을 하나의 워크스페이스에서 운용하는 AI 데스크탑 클라이언트

<details>
<summary><b>상세 내용 및 기술적 성취 (클릭)</b></summary>

<details>
<summary><b>Troubleshooting (기술적 문제 해결 및 아키텍처 고민) 이후3개만 남기고 다뺄거임</b></summary>

---

</details>
</details>

---
