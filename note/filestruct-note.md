### 1장
#### 주요 용어
| 주요 용어                                                  | 설명                                                                                                     |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **레코드 어커런스<br>(record occurrence)**                    | - 한 레코드 타입의 인스턴스(instance)<br>- 레코드 타입의 각 필드에 따라 실제 값이 들어가 어떤 특정 객체를 나타내는 것<br>- 일반적으로 레코드(record)라고 함 |
| **레코드 타입 <br>(record type)**                           | - 논리적으로 서로 연관된 데이타 필드(항목)들의 집합<br>- 엔티티 타입                                                             |
| **데이터 필드(field)<br>애트리뷰트(attribute)<br>데이터 항목 (item)** | - 이름을 가진 논리적 데이타의 최소 단위<br>- 특정 객체(object, entity)의 한 성질의 값                                            |
| **화일(file)**                                           | - 보조기억장치에 저장된 같은 종류의 레코드 집합<br>- 하나의 응용 목적을 위해 함께 저장된 레코드                                              |

#### 파일의 종류 및 파일 구조 선정

| ★ 파일의 종류                           | 설명                                                                                                                                                                                                                                     |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **마스터 파일 <br>(master file)**       | - 어느 한 시점에서 조직체의 업무에 관한 정적인 면을 나타내는 데이타의  집합<br>- 비교적 영구적(permanent)인 데이타, 즉 역사적 데이타 (historical status data)를 포함<br><br>★ 사전 화일 (dictionary file)<br>- 마스터 화일의 특수한 형태<br>- 데이타에 대한 기술(description) - 타입, 크기, 이름, 활용 등과 데이터에 대한 설명을 보관 |
| **트랜잭선 파일 (transaction file)**     | - 마스터 화일의 변경 내용을 모아 둔 화일<br>- 마스터 화일을 변경(update)하기 위한 데이타 화일<br>- insert, delete, modify, replace<br><br>★ 트랜잭션 (transaction)<br>- 논리적인 작업 단위<br>- 하나의 건수로 처리되어야 하는 분리될 수 없는 단일 작업                                                     |
| **보고서 파일 <br>(report file)**       | - 사용자에게 정보 검색 결과를 보여주기 위해 일정한 형식을 갖춘 데이터를 저장하고 있는 파일<br>- 화면에 디스플레이, 하드 카피 보고서 출력                                                                                                                                                      |
| **작업 파일 <br>(work file)<br>**      | - 어느 한 프로그램에서 생성된 출력 데이타를 다른 프로그램의 입력 데이터로 사용하기 위해 임시로 만드는 파일(temporary file)<br>-  시스템이 자동으로 만드는 작업 화일 예 : 정렬을 위한 파일<br>-  프로그램이 만드는 작업 화일 예 : 수강신청 변경 파일                                                                             |
| **프로그램 파일 <br>(program file)<br>** | - 데이타를 처리하기 위한 명령어들을 저장하고 있는 화일<br>- 고급언어(C, JAVA), 어셈블리어, 작업 제어 언어(job control language) 등                                                                                                                                            |
| **텍스트 파일 <br>(text file)<br>**     | - 문자 숫자(alphanumeric)와 그래픽 데이타를 포함하고 있는 파일<br>- 텍스트 편집기의 입력과 출력으로 사용<br>- 여러 텍스트 편집기에 의해 처리될 수 있음                                                                                                                                      |
| **★ 파일 구조 선정 요소**                  | 1. 가변성<br>2. 활동성<br>3. 사용빈도수<br>4. 응답 시간<br>6. 화일 크기<br>5. 화일 접근 유형                                                                                                                                                                    |
| **데이터 파일 구성 이유**                   | - 메인 메모리에 전부 적재하기에는 양이 너무 많다.<br>- 특정 시간에 데이터의 일부만 접근하기 때문<br>- 별도로 저장시키면 데이터의 독립성을 유지할 수 있다.                                                                                                                                          |
|                                    |                                                                                                                                                                                                                                        |
| **★ 파일 사용 시 두가지  중요한 점**           |                                                                                                                                                                                                                                        |
| **1. 파일 사용의 형식**                   |                                                                                                                                                                                                                                        |
| 일괄처리(batch) 형식                     | - 마스터 화일 효율적으로 접근하도록 트랜잭션들을 구성함<br>- 트랜잭션들을 그룹화하여 처리하는 성능이 주요 관심사                                                                                                                                                                      |
| 대화(interactive) 형식                 | – 트랜잭션이 터미널에 도착하는 대로 구성하고 처리함<br>– 개별의 트랜잭션의 처리 성능이 주요 관심사                                                                                                                                                                             |
| **2. 파일 연산의 성격**                   |                                                                                                                                                                                                                                        |
| 연산의 순서                             | 생성, 기록(갱신,삽입,삭제), 판독, 삭제, 개방과 폐쇄(버퍼의 할당과 반환)                                                                                                                                                                                           |



---
### 2장
#### 저장장치

| 1차 저장 장치                                                          | 2차 저장 장치                              |
| ----------------------------------------------------------------- | ------------------------------------- |
| - 메인 메모리(DRAM \| 소멸성)<br>- 캐시 메모리(SRAM \| 소멸성)<br>- 플래시 메모리(비소멸성) | - 자기 디스크(비소멸성)<br>- 자기 테이프<br>- 광 디스크 |

| 하드 디스크(자기 디스크)     | **원체스터 디스크**                                                                                                                                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 분류 기준              | 기록의 표면 수, 데이타 전송률, 기록/판독 헤드 이동 시간, 회전 지연. 밀도                                                                                                                                             |
| 물리적 특성             | 디스크팩, 디스크 구동기, 디스크 제어기                                                                                                                                                                   |
| 디스크의 구성            | 트렉, 섹터, 갭, 실린더                                                                                                                                                                           |
| 블록                 | 디스크와 메인 메모리 사이의 전송되는 데이타의 논리적 단위<br>섹터에 저장, 크기(512byte, 1KB, 4KB)                                                                                                                        |
| ★ 유동 헤드 디스크        | 전송 연산 시간 = 탐구시간 + 헤드 활동 시간 + 회전 지연 시간 + 전송시간                                                                                                                                             |
| ★ 고정 헤드 디스크        | 전송 연산 시간 = 헤드 활동 시간 + 회전 지연 시간 + 전송시간                                                                                                                                                    |
| 하드웨어 장치의 특성 요소     | 1. 회전 속도<br>2. 디스크 드라이브 원반 수<br>3. 기록 면당 트랙 수<br>4. 트랙당 바이트 수                                                                                                                            |
| **블로킹**            |                                                                                                                                                                                          |
| 블로킹 이점             | - 갭으로 인한 기억 공간 낭비 감소<br>- I/O 시간의 감소                                                                                                                                                     |
| 블로킹 단점             | - 주 기억장치 내의 사용 공간 감소<br>- 블록의 일부 처리를 위해 블록 전체를 전송                                                                                                                                        |
| ★ 고정길이 블로킹         | - 공간 효율 낮고 처리가 간단.<br>- 길이만 알면 구분 가능                                                                                                                                                     |
| ★ (비)신장된 가변 길이 블로킹 | - 공간 효율 높고 처리가 많다.<br><br>- 분리 표시(레코드 끝 마크)<br>- 각 레코드 앞 길이 지시자 (시작 마크)<br>- 위치 테이블 (포인터)                                                                                                |
| **고려 사항**          | 적재 밀도, 균형 밀도, 집약성                                                                                                                                                                        |
|                    |                                                                                                                                                                                          |
|                    |                                                                                                                                                                                          |
| **자기 테이프**         | **순차 접근 저장 장치**                                                                                                                                                                          |
| 테이프 구동기            | - 판독/기록 헤드 : 그림 2.13 , 2.14 참조 <br>- 판독/기록 : 테이프의 자화 표면과 헤드의 자속 (magnetic flux) 사이의 상호 작용<br>- 적재점(load point), 테이프 끝 표시(end-of- tape-mark)                                              |
| 기록 밀도              | - 1인치당 비트수(bpi : bits per inch) <br>- 1바이트 : 한 컬럼에 평행적으로 기록할 수 있는 여러 개의 비트로 이루어진 단위, 보통 8비트 <br>- 9트랙 테이프 : 8트랙의 데이타 + 1트랙의 오류 제어 비트(parity bit) <br>- 1,600bpi, 6,250bpi, 30,000bpi(최근) |
| 블록 간 갭(IBG)        | - 테이프 이동 속도 조절 (0.3~0.75inch) – 가속 시간과 감속 시간 제공                                                                                                                                          |
| 블로킹 인수             | - 공간 활용도와 접근 시간과 관련 <br>- 버퍼의 크기를 감안하여 결정                                                                                                                                                |
|                    |                                                                                                                                                                                          |
| **★ 블로킹**          |                                                                                                                                                                                          |
| 블로킹을 안한 경우         | 소요 길이(inch) = (byte/bpi + IBG) x 레코드 수                                                                                                                                                   |
| 블로킹을 한 경우          | 소요 길이(inch) = (블록 수 x byte/bpi + IBG) x 레코드 수/블록 수                                                                                                                                       |
|                    |                                                                                                                                                                                          |
|                    |                                                                                                                                                                                          |
| **광 디스크**          |                                                                                                                                                                                          |
| ★ 저장 원리            | pit(구멍) 방식, bubble 방식                                                                                                                                                                    |
| ★ 판독 방식            | CLV방식(가변 모터 속도), CAV방식(일정 모터 속도, 튼튼, 빠름)                                                                                                                                                 |
|                    |                                                                                                                                                                                          |
|                    |                                                                                                                                                                                          |
| **RAID**           | **디스크의 병렬 연결**                                                                                                                                                                           |
| ★ 사용 이유            | 데이타의 판독과 기록 속도 개선, 신뢰성 증진                                                                                                                                                                |
| ★이점                | 효율적인 비용, 고도의 신뢰성과 고속의 데이타 전송률                                                                                                                                                            |






---
### 3장
| 파일 디렉터리                                          | 설명                                                                                            |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| **계층 디렉터리 구조**                                   | 동일한 접근 방법으로 장치에 상관없이 접근 가능<br><br>- 심벌 테이블                                                    |
| **★프로그렘의 파일 READ 요청 시 작업**                       | 1. 프로그램<br>2. 채널 프로그램<br>3. 채널<br>4. 제어 장치<br>5. 입출력 장치<br>6. 버퍼<br>7. 채널<br>8. 입출력 제어기->프로그램 |
|                                                  |                                                                                               |
| **★ 단순 버퍼 시스템 알고리즘**                             |                                                                                               |
| **생산자 루틴 : 응용**(버퍼 데이터 구역 n 개)                   | **소비자 루틴: 채널**(버퍼 데이터 구역 n 개)                                                                 |
| `loop: if(full_flag = 1) goto loop;`             | `wait: if(full_flag = 0) goto wait;`                                                          |
| `   issue start-I/O command to disk-controller;` | `    read buffer into work area;`                                                             |
| `    wait while buffer is being filled;`         | ***`    record_counter += 1;`***                                                              |
| ***`    record_counter = 1;`***                  | ***`    if(record_counter > n) full_flag = 0;`***                                             |
| `    full_flag = 1;`                             | `    goto wait;`                                                                              |
| `    goto loop;`                                 |                                                                                               |
|                                                  |                                                                                               |
| **★ 이중 버퍼 시스템 알고리즘**                             |                                                                                               |
| **생산자 루틴 : 응용**                                  | **소비자 루틴: 채널**                                                                                |
| `loop: if(to_fill.full_flag = 1) goto loop;`     | `wait: if(to._empty.full_flag = 0) goto wait;`                                                |
| `   issue start-I/O command to disk-controller;` | `read record[to_empty.record_counter] into work area;`                                        |
| `    wait while to_fill.buffer is being filled;` | `    to_empty.record_counter += 1;`                                                           |
| `    to_fill.record_counter = 1;`                | `    if(to_empty.record_counter > n){`                                                        |
| `    to_fill.full_flag = 1;`                     | `    to_empty.full_flag = 0;`                                                                 |
| `    to_fill = to_fill.next_buffer;`             | `    to_empty = to_empty.next.buffer; }`                                                      |
| `    goto loop;`                                 | `    goto wait;`                                                                              |

---
### 4장
순차파일 키순차파일 갱신처리

| **키 순차 파일**    | 설명                                                                                                                                                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **트랜잭션 코드**    | 레코드에서 키값과 트렌젝션 코드만 있으면 된다.                                                                                                                                                                                                                                                           |
| **★ 종류**       | 새 레코드 삽입( I )<br>기존 레코드의 삭제( D )<br>기존 레코드의 수정( C )                                                                                                                                                                                                                                  |
| **★ 갱신 알고리즘**  | - transKey : 트랜잭션 화일의 레코드 키 <br>- masterKey : 마스터 화일의 레코드 키 <br>- 가정 : 화일의 끝을 나타내는 EOF는 어떤 레코드 키 값보다 크다<br><br>- 마스터 파일과 트랜잭션 파일을 비교<br>- 어느 한 키 값이 두 파일에서 일치하면 갱신 프로그램은 갱신 코드(I,D,C)에 따라 레코드를 수정 또는 삭제<br>- 트랜잭션 레코드 키 값이 마스터 파일의 어떤 레코드의 것과도 일치하지 않으면, 새로 삽일할 레코드로 간주하고 마스터 파일에 삽입 |
| **오류 처리**      | - 마스터 화일에 있는 키 값을 가진 레코드를 삽입 <br>- 마스터 화일에 없는 키 값을 가진 레코드를 삭제<br>- 마스터 화일에 없는 키 값을 가진 레코드를 수정                                                                                                                                                                                        |
| **임의 갱신 알고리즘** | - 해당 마스터 레코드의 위치를 찾고, 이 마스터 레코드에 트랜잭션을 적용하고, 갱신된 마스터 레코드를 원래의 위치에 다시 기록<br>- 효율적 : 해당 마스터 레코드만 읽고, 원 위치에 재기록 <br>- 임의 접근이 가능해야 한다. <br>- 레코드 삭제 : 물리적 제거보다 해당 레코드 위에 “deleted” 표시를 기록하여 논리적 삭제로 대신하는 게 낫다.                                                                           |


---
### 5장
대체선택 자연선택 과정 쓰기
