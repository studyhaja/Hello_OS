### Remind
Context Switching은 비용이 크므로 줄이는 것이 좋은데 줄이는 방법 중에 하나가 스레드이다.

## Process와 Thread
프로세스는 자원을 할당 받고 자원을 제어하여 작업(목적)을 달성한다. 즉, 프로세스를 실행하기 위해서는 자원과 제어가 필요하다.
![](https://images.velog.io/images/langssi/post/1f376bb8-2174-4188-8491-5e6c0df3a4b8/image.png)
1. 자원 
2. 제어

두 부분 중 제어 부분만 따로 떼어 놓은 것이 스레드이다.(`~`과 같은 실모양으로 스레드를 표현한다.)
![](https://images.velog.io/images/langssi/post/fc26e8fc-0468-4d22-8900-ae7b1757a98e/image.png)
프로세스 하나(가마할아범)에 스레드(팔)는 여러개가 있을 수 있다(제어가 여러개 있을 수 있다).

## Thread
- 스레드는 리소스를 제어한다.
- 자원은 공유되고 스레드는 독립적이다.
![](https://images.velog.io/images/langssi/post/e78e257e-d35a-40f8-a1ad-cee82fdfc6c5/image.png)

### 리소스
- 프로그램 코드(프로그램 카운터PC가 어디 실행하는지 가르키고 있음)
- 작업을 하기 위한 데이터
- 전역적으로 사용하는 데이터들이 heap에 저장
### 제어
- 다양한 제어 정보 - PC, 상태 정보, SP(Stack Pointer)
- 지역 데이터(for문을 쓰면 안에서 데이터를 만들어서 사용하고 for문 안에서(지역에서만) 유효) 
  - 지역데이터를 사용하는 이유는 제어를 위함임, 지역 데이터는 스택 영역에 저장됨

### 스레드 특징
- Light Weight Process (LWP)
  - 무게가 가벼운 프로세스 -> 프로세스는 자원과 제어를 각각 가지고 있는데 스레드는 자원은 공유하고 제어부분만 갖고 있으므로
- 프로세서(e.g, CPU) 활용의 기본 단위
  - 스레드가 여러 개 있으면 각각의 프로세서를 활용하게 됨 -> 스레드가 여러개면 동시에 여러개의 CPU를 사용할 수 있다.
- 구성 요소
  - Thread ID
  - Register Set(PC, SP 등)
  - Stack (i.e. Local  Data)
- 제어 요소 외 코드, 데이터 및 자원들은 프로세스 내 다른 스레드들과 **공유**
- 전통적 프로세스 = 단일 스레드 프로세스
  - 프로세서에 제어가 하나

### 메모리 관점
![](https://images.velog.io/images/langssi/post/43430be4-9afa-4df6-9f6c-0f81d80bf45c/image.png)

### Single-thread vs Multi-threads
![](https://images.velog.io/images/langssi/post/2619b836-c4b3-4937-b58c-592a48f38546/image.png)
![](https://images.velog.io/images/langssi/post/53ec249b-283b-476e-a343-f8e7874dc2e6/image.png)

## 스레드의 장점
### 사용자 응답성(Responsiveness)
- 일부 스레드의 처리가 지연되어도 다른 스레드는 작업을 계속 처리 가능
### 자원 공유(Resource Sharing)
- 자원을 공유해서 효율성 증가(커널의 개입을 피할 수 있음)
  - ex. 동일 address space에서 스레드 여러개
  - 커널 개입 자체가 굉장히 큰 오버헤드이다.
  - <-> context switch는 자원을 공유하지 않음(p1이 자원을 쓰고 있을때 p2는 대기) + 비용이 많이 발생
### 경제성(Economy)
- 프로세서의 생성, context switch에 비해 효율적
### 멀티 프로세서(multi-processor) 활용
- 스레드 여러개 -> 여러개의 cpu core를 동시에 사용할 수 있다.
- 병렬처리를 통해 성능 향상

## 스레드 사용의 예
![](https://images.velog.io/images/langssi/post/b58aca95-866a-4560-9906-a07a88ee9ead/image.png)
### 스레드가 하나

- I/O 발생 -> `run`에서 `block` 상태로 변함
- 예시
  - 화면을 출력하고 있을때 마우스를 돌리는 순간 화면이 멈추고 마우스가 다 돌아가고 나서 화면이 재생
  - 말을 하면 화면도 안나오고 마우스도 안먹음
  -> 하나의 작업을 하는중에 다른 작업을 할 수 없음, 제대로 된 게임 불가
- 스레드를 3개 만들어서 각각 처리(사용자 입력, 화면 출력, 스피커/마우스 입력)하게 함
  - 자원들은 공유하게 되므로 게임을 원활히 할 수 있음 => 사용자 응답성이 올라감
- 같은 의미로 프레젠테이션 재생, 문서작업, 임시 저장이 동시에 가능한 것은 여러개의 스레드가 자원을 공유해서 작업하고 있기 때문임

## 스레드의 구현
### 사용자 수준 스레드(User Thread)
- 커널은 제어하기 위한 스레드를 하나 만들고(커널 수준의 스레드) 내부적으로는 라이브러리를 사용해서 여러개의 스레드를 사용하는 것처럼 동작하며 스레드 제어 블록이 생성되어 있음 
- 커널 수준 스레드는 하나인데 사용자 수준 스레드는 여러개로 다대일 관계가 형성
![](https://images.velog.io/images/langssi/post/de3eff01-d315-4aa4-b4b8-3f67f5e5f172/image.png)
- 사용자 영역의 스레드 라이브러리로 구현 됨(라이브러리로 스레드처럼 돌아갈 수 있게 만든것)
  - 스레드의 생성, 스케줄링 등
  - POSIX threads, Win32 threads, Java thread API 등
- 커널은 스레드의 존재를 모름
  - 커널의 관리(개입)을 받지 않음
    - 생성 및 관리의 부하가 적음, 유연한 관리 가능
    - 이식성(portability)이 높음 (라이브러리만 있으면 만든 멀티스레드 프로그램을 그대로 사용할 수 있음)
  - 커널은 프로세스 단위로 자원 할당
    - 하나의 스레드가 block 상태가 되면 모든 스레드가 대기(single-threaded kernel의 경우)
### 커널 수준 스레드(Kernel Threads)
![](https://images.velog.io/images/langssi/post/62bbf4d2-d00e-46f5-b0b1-3b3a467fd345/image.png)
사용자 수준 스레드의 갯수만큼 커널에서도 스레드가 생성됨 -> 1:1 매핑
- OS(Kernel)가 직접 관리
- 커널 영역에서 스레드의 생성, 관리 수행
  - Context Switching 등 부하(Overhead)가 큼
    - CPU를 사용하기 위해서는 스레드 간 context switching이 필요, 프로세스 간 context switching 보다는 적긴 하지만 오버헤드가 발생므로 사용자 수준 스레드보다는 무거움
- 커널이 각 스레드를 개별적으로 관리
  - 프로세스 내 스레드들이 병행 수행 가능
    - 하나의 스레드가 block 상태가 되어도, 다른 스레드는 계속 작업 수행 가능
      
## Multi-Threading Model
n:1 모델(사용자 수준 스레드), 1:1 모델(커널 수준 스레드) 모두 단점이 있다 -> 둘을 섞자 -> n:m 모델(혼합형 스레드)
### 혼합형(n:m) 스레드
- n개 사용자 수준 스레드, m개의 커널 스레드(n > m)
  - 사용자는 원하는 수만큼 스레드 사용
  - 커널 스레드는 자신에게 할당된 하나의 사용자 스레드가 block 상태가 되어도, 다른 스레드 수행 가능
    - 병행 처리 가능
- 효율적이면서도 유연함
![](https://images.velog.io/images/langssi/post/7cc086d4-49ba-4a4f-b5a5-4619c4508d73/image.png)
- 사용자는 스레드를 자유롭게 사용하고 스레드 라이브러리가 관리
- 커널 수준 스레드에서는 사용자 수준 스레드에게 동적으로 자원을 쓸 수 있도록 관리함
  - 하나의 스레드가 블록이 되어도 다른 스레드가 정상적으로 작동할 수 있음
- OS들이 실제 사용하는 모델은 혼합 스레드형 모델이다.