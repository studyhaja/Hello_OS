## Process Management
### Job/Program
- 실행할 프로그램 + 데이터
- 컴퓨터 시스템에 실행 요청 전의 상태(디스크에 보관된 상태)

### Process
- 실행을 위해 시스템(커널)에 등록된 작업
- 시스템 성능 향상을 위해 커널에 의해 관리 됨(-> 운영 체제의 역할 달성)
![](https://images.velog.io/images/langssi/post/7074943a-17c0-4bcd-83a3-2e9ed6cbd6db/image.png)
## 프로세스의 정의
### 실행중인 프로그램
- 커널에 등록되고 커널의 관리하에 있는 작업
- 각종 자원들을 요청하고 할당 받을 수 있는 개체
- 프로세스 관리 블록(PCB)을 할당 받은 개체
- 능동적인 개체(active entity)
  - 실행 중에 각종 자원을 요구, 할당, 반납하며 진행

### Process Control Block(PCB)
- 커널 공간(kernel space) 내에 존재
- 각 프로세스들에 대한 정보를 관리

![](https://images.velog.io/images/langssi/post/af16dcb0-41aa-4980-b9a1-b38ee79adaa2/image.png)

## 자원(Resource)의 개념
- **커널의 관리 하**에 프로세스에게 할당/반납 되는 수동적 개체(passive entity)
### 자원의 분류
- H/W Resources
  - Processor, Memory, Disk, Monitor, Keyboard, Etc.
- S/W Resources
  - Message, Signal, Files, Installed SWs, Etc.
    
## Process Control Block(PCB)
- OS가 프로세스 관리에 필요한 정보 저장
- 프로세스 생성시에 생성 됨
![](https://images.velog.io/images/langssi/post/e4d92217-c946-4b40-acec-d32be98f2dd8/image.png)
### PCB가 관리하는 정보
- PID(Process Idification Number)
  - 프로세스 고유 식별 번호
- 스케줄링 정보
  - 프로세스 우선순위 등과 같은 스케줄링 관련 정보들
- 프로세스 상태
  - 자원 할당, 요청 정보 등
- 메모리 관리 정보
  - Page table, Segment table 등
- 입출력 상태 정보
  - 할당 받은 입출력 장치, 파일 등에 대한 정보 등
- 문맥 저장 영역(Context Save Area)
  - 프로세스의 레지스터 상태를 저장하는 공간 등
- 계정 정보
  - 자원 사용 시간 등을 관리

[참고]
- PCB 정보는 OS 별로 서로 다름
- PCB 참조 및 갱신 속도는 OS 성능을 결정짓는 중요한 요소 중 하나

## 프로세스 상태(Process States)
- 자원 간의 상호 작용에 의해 결정
### 프로세스 상태 및 특성
![](https://images.velog.io/images/langssi/post/b611935d-360a-4664-9508-e3207364b913/image.png)뒤에서 자세히

## Process State Transition Diagram
![](https://images.velog.io/images/langssi/post/a4886505-f13e-4fc4-80b1-2b6e2e3366db/image.png)
복잡..하나씩 살펴보자

### Created State
- 작업(Job)을 커널에 등록
- PCB 할당 및 프로세스 생성
- 커널
  - 가상 메모리 공간 체크 및 프로세스 상태 전이(Ready or Suspended ready)

![](https://images.velog.io/images/langssi/post/4f21c664-e945-4001-a8f3-422e66b7365b/image.png)
메모리가 있는가 없는가에 따라 ready/suspended ready

### Ready State
- 프로세서 외에 다른 모든 자원을 할당 받은 상태
  - 프로세서(CPU) 할당 대기 상태
  - 즉시 실행 가능 상태
- Dispatch(or Scheduled)
  - Ready state -> Running state

![](https://images.velog.io/images/langssi/post/f608763b-9594-4afa-99a3-a52016742727/image.png) 프로세서를 할당 받으면 dispach, schedule 되었다고 한다.

### Running State
- 프로세서와 필요한 자원을 모두 할당 받은 상태
- Preemption
  - Running State -> Ready State(프로세서를 뺐겼을때)
  - 프로세서 스케줄링(e.g, time-out, priority changes)
- Block/Sleep
  - Running state -> asleep state
  - I/O 등 자원 할당 요청하고 대기 (ex. 은행에서 서류를 놓고와서 가지고 올때까지 대기한다.)
  
![](https://images.velog.io/images/langssi/post/8272d391-9acc-45b9-93cd-e653c1e478aa/image.png)

### Blocked/Asleep State
- 프로세서 외에 다른 자원을 기다리는 상태
  - 자원 할당은 System Call에 의해 이루어 짐
- Wake-up
  - Asleep state -> Ready State
  
![](https://images.velog.io/images/langssi/post/c4ae5e86-0258-459d-9653-902ee4db7f85/image.png)
자원을 받았다고 해도 running 중인 다른 프로세스에 바로 끼어들 순 없다. ready 상태로 돌아가서 다음 CPU 할당을 기다려야 한다.

### Suspended State
- Suspended -> 메모리를 할당 받지 못한(빼앗긴) 상태
  - Memory image(메모리의 상태를 찍어놓은 것)를 swap device(일종의 하드 디스크)에 보관(swap-out) -> 메모리 할당시 바로 복구(swap-in)하기 위하여
   *swap device: 프로그램 정보 저장을 위한 특별한 파일 시스템
   - 커널 또는 사용자에 의해 발생
- Swap-out(suspended), Swap-in(resume)
![](https://images.velog.io/images/langssi/post/bf26d96a-b68d-4d8d-a101-bebaefda0211/image.png)

### Terminated/Zombie State
- 프로세스 수행이 끝난 상태(종료되기전 들리는 상태)
  - Why? 다음에 비슷한 작업이 들어왔을때 관리하기 쉽게 하기 위해서
- 모든 자원 반납 후
- 커널 내에 일부 PCB 정보만 남아있는 상태
  - 이후 프로세스 관리를 위해 정보 수집
  - 커널이 정보 수집이 끝나면 프로세스 삭제 후 종료
    
## 프로세스 관리를 위한 자료구조
- Ready Queue
- I/O Queue
- Device Queue
![](https://images.velog.io/images/langssi/post/2a3dd470-d66a-41bd-b6b9-fe7e3566d1a0/image.png)