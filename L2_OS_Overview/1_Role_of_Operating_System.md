## 운영체제
컴퓨터 하드웨어를 효율적으로 관리하여 사용자/응용프로그램에게 서비스를 제공한다.

## 운영체제의 역할
### User Interface(편리성)
사용자가 시스템을 편리하게 사용할 수 있도록 편리성 제공
- CUI(Character User Interface)
    - 문자기반인 과거에 주로 사용되던 유저 인터페이스
- GUI(Graphical User Interface)
    - 현재 사용되는 그림 형태 기반의 유저 인터페이스
- EUCI(End-User Comfortable Interface)
	- 특별한 목적을 위해서 만들어진 기기의 경우 목적만을 위해 사용자가 편하게 사용할 수 있도록 특화된 인터페이스
    - ex. mp3 player (mp3 사용만을 위한 인터페이스)
    
### Resource Management(효율성)
주어진 자원을 제대로 활용하여 효율성을 높임
- HW Resource(processor, memory, I/O devices, Ect.)
- SW Resource(file, application, message, signal, Etc.)

### Process and Thread Management
프로세스를 관리하는 역할

*Process: 프로그램을 실행하는 주체

### System Management(시스템 보호)
사용자가 불법적인 형태로 시스템을 사용하려고 할때 그로부터 보호함

## 컴퓨터 시스템의 구성
![image](https://user-images.githubusercontent.com/45524783/114297543-1d54fb00-9aec-11eb-8a97-7113b9b3ffb6.png)
### Kernel
운영체제의 핵심을 모아놓은 것(뒤에서 자세히)
### System Call Interface
- 사용자가 직접 커널을 엑세스하거나 조작하면 OS가 하드웨어를 제어하는데 문제를 야기할 수 있으므로 필요한 기능이 있을때 커널에 요청을 하는 통로
- 즉, 커널이 제공하는 기능들 중 사용자가 사용할 수 있는 기능들을 모아놓은 것들
### 커널이 하는 일들
![image](https://user-images.githubusercontent.com/45524783/114297565-35c51580-9aec-11eb-9a8f-d68965fb2609.png)

## 운영체제의 구분
### 동시 사용자수
- Single-user System
	- 한 명의 사용자만 시스템 사용 가능
      - 한 명의 사용자가 모든 시스템 자원 독점
      - 자원 관리 및 시스템 보호 방식이 간단
    - 개인용 장비(PC, mobile) 등에 사용
      - Windows 7/10, Android, MS-DOS 등
- Multi-user System
    - **동시에** 여러 사용자들이 시스템 사용 
      - 각종 시스템 자원(파일 등)들에 대한 소유 권한 관리가 필요
      - OS 기능 및 구조가 복잡
    - 서버, 클러스터 장비 등에 사용
	  - Unix, Linux, Windows server등
    - 동시에 여러 프로세스가 실행될 수 있음
### 동시 실행 프로세스 수
- 단일 작업(Single-tasking System)
  - 시스템 내에 하나의 작업(프로세스)만 존재
    - 하나의 프로그램 실행을 마친 뒤에 다른 프로그램을 실행
  - 운영체제의 구조가 간단
  - ex. MS-DOS
- 다중 작업(Multi-tasking System)
  - 동시에 여러 작업(프로세스)의 수행 가능
    - 작업들 사이의 동시 수행, 동기화 등을 관리해야 함
  - 운영체제의 기능 및 구조가 복잡
  - ex. Unix/Linux, Windows 등

### 작업 수행 방식(사용자가 느끼는 사용 환경)
- Batch Processing System
- Time-sharing System
- Distributed Processing System
- Real-time System



#### 1. 아주 옛날 os가 없던 시절에는 순차 처리 사용했다(~1940s)
- 운영체제 개념 x
- 사용자가 기계어로 직접 프로그램 작성
- 각 작업을 순차적으로 처리함
- 단점: 각 작업에 대한 준비 시간 소요
- 예를 들어 (정말 예일 뿐임) 1번 작업은 java면 java를 위한 준비를 해야됨.<br>
그 후 python작업이 2번이면 이것에 대한 작업을 또 해야됨. 
- 이런 단점을 보안하고자 나온 것이 batch system

#### 2. Batch processing system(일괄 처리 시스템, 1950s~1960s)
- 모든 시스템을 중앙(전사계산소 등)에서 관리 및 운영
- 사용자의 요청 작업(천공카드 등)을 일정 시간 모아 두었다가 한번에 처리
- 시스템 지향적(systme-oriented, 시스템에게 유리한, 유저에게 불리한)
- 장점
  - 많은 사용자가 시스템 자원 공유
  - 처리 효율(throughput)향상
-단점
  - 생산성(productivity) 저하
    - 같은 유형의 작업들이 모이기를 기다려야 함
  - 긴 응답시간(turnaround time)
    - 약 6시간(작업 제출에서 결과 출력까지의 시간)
![](https://images.velog.io/images/kpl5672/post/9d79d39e-0b41-4b29-b28b-f969eb86bb1d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.41.08.png)
#### 3. Time-sharing system(시분할 시스템, 1960s~1970s)
- 여러 사용자가 자원을 동시에 사용
  - OS가 파일 시스템 및 가상 메모리 관리
- 사용자 지향적(User-oriented)
  - 대화형(conversational, interacitve) 시스템 (사용자 입장에서 그렇게 느낌)
  - 단말기(CRT terminal) 사용
- 장점
  - 응답시간 단축(약 5초)
  - 생산성(productivity) 향상
    - 프로세서 유휴 시간 감소
- 단점
  - 통신 비용 증가
    - 통신선 비용, 보안 문제 등
  - 개인 사용자 체감 속도 저하
    - 동시 사용자수 증가 -> 시스템 부하 증가 -> 느려짐 (개인관점에서)
![](https://images.velog.io/images/kpl5672/post/a9b462fc-535f-45c8-bb43-1765aff42574/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.43.13.png)
#### 4. Personal Computing
- 개인이 시스템 전체 독점
- CPU 활용률이 더이상 고려의 대상이 아님(원래는 최대한 컴퓨터를 놀지 않고 일시키는 게 주 관심사였음)
- os가 상대적으로 단순(하지만 다양한 편리한 기능 지원)
- 장점
  - 빠른 응답시간
- 단점
  - 성능이 낮음
 
#### 5. Parallel Processing System
- 단일 시스템 내에서 둘 이상의 프로세서 사용
  - 동시에 둘 이상의 프로세스 지원
- 메모리 등의 자원 공유(Tightly-coupled system)
- 사용 목적
  - 성능 향상
  - 신뢰성 향상(하나가 고장나도 정상 동작 가능)
- 프로세서간 관계 및 역할 관리 필요
![](https://images.velog.io/images/kpl5672/post/208a7336-0b8e-460c-b9b5-4d068305155d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.48.27.png)
#### 6. Distributed processing system(분산 처리 시스템)
- 네트워크를 기반으로 구축된 병렬처리 시스템(Loosely-coupled system)
  - 물리적인 분산, 통신망 이용한 상호 연결
  - 각각 컴퓨터를 노드라고 부름
  - 각각 운영체제 탑재한 다수의 범용 시스템으로 구성
  - 사용자는 분산운영체제를 통해 하나의 프로그램, 자원처럼 사용 가능(은폐성, transparency)
  - 각 구성요소들간의 독립성 유지, 공동작업 가능
  - cluster system, client-server system, P2P 등
- 장점
  - 자원 공유를 통한 높은 성능
  - 고신뢰성, 높은 확정성
- 단점
  - 구축 및 관리가 어려움
![](https://images.velog.io/images/kpl5672/post/eb442976-680e-4cdf-9e35-190f231fcee5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.50.52.png)
#### 7. Real-time system(실시간 시스템)
- 작업 처리에 dealine을 갖는 시스템
  - 제한 시간 내에 서비스를 제공하는 것이 자원 활용 효율보다 중요
- 작업 종류
  - Hard real-time task
    - 늦으면 큰일나는 거. 
    - 예, 발전소 제어, 무기 제어
  - Soft real-time task
    - 동영상 재생
  - Non real-time task

