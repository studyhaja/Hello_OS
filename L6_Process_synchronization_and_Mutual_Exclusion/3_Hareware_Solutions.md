# HW Solutions
## Synchronization Hardware
### TestAndSet(TAS) Instruction
- Test와 Set을 한번에 수행하는 기계어
- Machine Instruction
  - Atomicity, Indivisible
  - **실행중 interrupt를 받지 않음(preemption 되지 않음)**
- Busy Waiting
  - Inefficient
  
## TAS Instruction
![](https://images.velog.io/images/langssi/post/a1e88442-7462-4fc1-a106-819e45f9443e/image.png)
- target에 있는 값을 temp에 넣어주고 target=true로 만들고 temp를 리턴
- 타겟의 현재 값을 반환하면서 target은 true로 만든다 -> 모든 작업이 한번에 수행됨
## ME with TAS Instruction
![](https://images.velog.io/images/langssi/post/2d15c3ab-340e-4400-9f4b-3e1c84ed5e5e/image.png)
- 초기 lock의 값이 false 이므로 TAS(lock)은 false를 return하고(-> CS 진입) lock=true로 바뀜
- 이후 다른 프로세스에서 TAS(lock)을 하면 lock이 true이므로 while문을 계속 돌면서 대기하게 됨
- cs에 있던 프로세스가 끝나면 lock=false로 변환하고 대기하고 있던 프로세스는 TAS(lock)이 false가 되므로 cs에 진입 가능

=> SW solution에서는 복잡하게 해결했는데 HW에서 한번에 수행되는 것을 보장해줌으로서 문제가 간단히 해결됨

### Bounded Waiting 위배
![](https://images.velog.io/images/langssi/post/033463c0-cceb-41cd-a59b-cfd4b6b9c0a8/image.png)
- while문에 다시 돌아오는 시간에 따라 한 프로세스가 계속 cs에 못들어가는 상황이 생길 수 있음

### N-Process Mutual Exclusion
![](https://images.velog.io/images/langssi/post/72f1d266-d3d0-4be6-82ea-ebb7075f34c8/image.png)
- waiting 값을 사용하여 가까운 프로세스 먼저 진입할 수 있도록 함
  - `j = (i+1) % n` => 자신 뒤의 프로세스들을 확인
  - 뒤의 프로세스에서 대기 중이라면 다음 순서로 진입할 수 있도록 `waiting[j] = false`로 바꿈
  - 대기중인 프로세스가 없다면 `lock=false`로 바꿔서 다른 프로세스가 들어올 수 있도록 함
  
## HW Solution
### 장점
- 구현이 간단
### 단점
- Busy Waiting
  - `While(TAS(lock))` ...
  - Inefficient
### Busy waiting 문제를 해소한 상호배제 기법
- Semaphore
  - 대부분의 OS들이 사용하는 기법
