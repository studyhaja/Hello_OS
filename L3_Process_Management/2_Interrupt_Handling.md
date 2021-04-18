## Interrupt
- **예상치 못한**, **외부**에서 발생한 이벤트(unexpected, external events)
  - 누가 옆에서 쿡 찌르는 것 (예상하지 못한 것)
### 인터럽트의 종류
- I/O interrupt
  - 예상하지 못한 순간의 마우스 클릭, 키보드 클릭 등..
- Clock Interrupt
  - CPU clock이 발생할 때 남
- Console Interrupt
  - 콘솔 창에서 발생
- Program Check Interrupt
  - 프로그램에서 문제가 있으면 발생
- Machine Check Interrupt
  - 하드웨어가 문제가 있을때 발생
- Inter-process Interrupt
  - 다른 프로세스가 쿡 찌르는 것
- System call Interrupt
  - 시스템 콜에 의한 것
  

## 인터럽트 처리 과정
![](https://images.velog.io/images/langssi/post/44e0a8b7-f43f-452b-88f5-c16d338ffd9a/image.png)

책을 펴놓고 공부를 하고 있었는데 누가 방해함 -> 어디까지 공부하고 있었는지 책갈피를 꽂아둠 (흐름을 저장)

![](https://images.velog.io/images/langssi/post/d01fe63e-97b1-448f-94b3-54779dea94ae/image.png)
커널 개입 -> 인터럽트 발생 장소, 원인 파악 -> 어떤 서비스를 호출해야하는지 파악 -> 실제로 서비스 함(해당 프로그램을 실행하는 프로세서를 프로세서에 넣어줌) -> 끝나면 프로세서가 비어있고 ready 상태 중 하나를 넣어주게 됨(아까 중단된 프로세스가 무조건 들어오는게 아님) -> 순서가 되면 원래의 프로세스가 실행되고 아까 꽃아둔 책갈피를 복구해서 중된된 일을 수행함

## Context Switching(문맥 교환)
### Context
- 프로세스와 관련된 정보들의 집합
  - CPU register context -> in CPU
  - Code & Data, Stack, PCB -> in memory
  
CPU가 작업을 처리할때는 반드시 레지스터에 데이터를 올린 후 레지스터에 있는 데이터로 작업을 해야한다. -> register context가 필요

![](https://images.velog.io/images/langssi/post/c9860003-1c1b-4b5b-97f4-18ca2603761b/image.png)
프로세서가 CPU에서 일을 하고 있다가 인터럽트에 의해 또는 할당된 시간이 지나서 CPU를 뺏김 -> CPU에 저장된 것을 저장해두어야 함(CPU register context가 메모리 공간(PCB)에 저장됨)
### Context Saving
- 현재 프로세서의 Register Context를 저장하는 작업
### Context Restoring
- Register Context를 프로세스로 복구하는 작업
### Context Switching
- Context Saving + Context Restoring
  - Pi가 CPU에서 나올때 PBCi에 context를 저장하고 CPU에 올라가는 Pj는 PCBj에 저장된 context를 복구함
- 즉, 실행 중인 프로세스의 context를 저장하고, 앞으로 실행할 프로세스의 context를 복구하는 일
  - 커널의 개입으로 이루어짐
## Context Switch Overhead
### 소요되는 비용
- OS마다 다름
- context switching은 자주 일어나고 있고 OS의 성능에 큰 영향을 줌
### 불필요한 Context Switching을 줄이는 것이 중요

- ex. 스레드(thread) 사용 등