## 4. 기본 스케줄링 알고리즘들
- FCFS(First-Come-First-Service)
- RR(Round-Robin)
- SPN(Shortest-Process-Next)
- SRTN(Shortest-Ramining time Next)
- HRRN(High-Response-Ratio Next)
- MLQ (Multi-level Queue)
- MFQ (multi-level Feedback Queue)

### FCFS(First-Come-First-Service)
- Non-preemptive scheduling
- scheduling criteria(기준)
  - ***도착 시간*** (ready queue 기준) 
  - 먼저 도착한 프로세스를 먼저 처리
- 자원을 효율적으로 사용 가능
- Batch system에 적합, interactive system에 부적함
- 단점
  - convoy effect
    - 하나의 수행시간이 긴 프로세스에 의해 뒤에 들어온 다른 프로세스들이 긴 대기시간을 갖게 되는 현상(대기시간 > 실행 시간)
  - 긴 평균 응답시간(response time)
![스크린샷 2021-04-16 오후 10 48 18](https://user-images.githubusercontent.com/70195733/115033847-da3cc280-9f05-11eb-9797-1210027d1316.png)
### RR(Round-Robin)
- Preemptive scheduling
- scheduling criteria
  - ***도착시간*** (ready queue 기준)
  - 먼저 도착한 프로세스를 먼저 처리
- 자원 사용 제한 시간(time quantum)이 있음
  - System parameter
  - 프로세스는 할당된 시간이 지나면 자원 반납(timer-runout)
  - 특정 프로세스의 자원 monopoly 방지
  - context switch overhead가 큼
  - 대화형, 시분할 시스템에 적합
#### Time quantum
- 시스템 성능을 결정하는 핵심 요소
- 한 텀에 주어지는 시간을 의미
- 너무 크면? -> 사실상 FCFS가 된다.
- 너무 작으면? -> processor sharing이 된다.
  - 사용자는 모든 프로세스가 각각의 프로세서 위에서 실행되는 것처럼 느낀다.
    - 첵마 프로세서 속도 - 실제 프로세서 성능의 1/n
  - High context switch overhead
![스크린샷 2021-04-16 오후 10 52 55](https://user-images.githubusercontent.com/70195733/115034468-8088c800-9f06-11eb-99a9-0036823df881.png)
### SPN(Shortest-Process-Next)
- Non-preemptive scheduling
- scheduling criteria: ***실행시간***
  - burst time이 가장 작은 프로세스를 먼저 처리
  - SJF(shortest job First) scheduling
  ![스크린샷 2021-04-17 오후 12 53 58](https://user-images.githubusercontent.com/70195733/115101050-114dbb00-9f7c-11eb-8bf2-184eedf22926.png)
- 장점
  - 평균 대기시간(WT) 최소화
  - 시스템 내 프로세스 수 최소화
    - 스케줄링 부하 감소, 메모리 절약 -> 시스템 효율 향상
  - 많은 프로세스들에게 빠른 응답 시간 제공
- 단점
  - starvation(무한대기) 현상 발생
    - BT가 긴 프로세스는 뒤로 계속 밀려서 자원 할당 못받을 수도 있음
      - Aging 등로 해결(HRRN)
  - 정확한 실행시간을 알 수 없음
    - 실행시간 예측 기법 필요
![스크린샷 2021-04-17 오후 12 57 28](https://user-images.githubusercontent.com/70195733/115101102-7c978d00-9f7c-11eb-9cd0-3adf27054f3d.png)
### SRTN(Shortest-Remaining time Next)
- SPN의 변형
- Preemptive scheduling
  - 잔여 실행 시간이 더 적은 프로세스가 ready 상태가 되면 선점됨
- 장점
  - SPN의 장점 극대화
- 단점
  - 프로세스 생성시, 총 실행 시간 예측이 필요함
  - 잔여 실행을 계속 추적해야 함 = overhead
  - context switching overhead
- 구현이 비현실적
### HRRN(High-Response-Ratio Next)
- SPN의 변형
  - SPN + Aging concepts
- Non-preemptive scheduling
- Aging Concepts
  - 프로세스의 대기 시간(WT)을 고려하여 기회를 제공
- scheduling criteria
  - Response ratio가 높은 프로세스 우선
![스크린샷 2021-04-17 오후 1 39 01](https://user-images.githubusercontent.com/70195733/115101846-54ab2800-9f82-11eb-94dc-75ac577618a8.png)
![스크린샷 2021-04-17 오후 1 39 54](https://user-images.githubusercontent.com/70195733/115101878-7e644f00-9f82-11eb-920b-a5c935242fe3.png)
### MLQ (Multi-level Queue)
- 작업(or 우선순위)별 별도의 ready queue를 가짐
  - 최초 배정된 queue를 벗어나지 못함
  - 각각의 queue는 자신만의 스케주링 기법 사용
- queue 사이에는 우선순위 기반의 스케줄링 사용
- 장점
  - 빠른 응답시간
- 단점
  - 여러 개의 queue관리 등 스케줄링 overhead
  - 우선순위가 낮은 queue는 starvation 현상 발생 가능
![스크린샷 2021-04-17 오후 1 42 47](https://user-images.githubusercontent.com/70195733/115101934-d602ba80-9f82-11eb-84e7-7be8bf753b30.png)
### MFQ (multi-level Feedback Queue)
- 프로세스의 queue간 이동이 허용된 MLQ
- Feedback을 통해 우선 순위 조정
  - 현재까지의 processor 사용 정보(패턴) 활용
- 특성
  - Dynamic priority
  - Preemptive scheduling
  - Favor short burst-time processes
  - Favor I/O bounded processes
  - Improve adptability
- 프로세스에 대한 사전 정보 없이 SPN, STRN, HRRN 기법의 효과를 볼 수 있음.
- 단점
  - 설계 및 구현이 복잡, 스케줄링 overhead가 큼
  - starvation 문제 등
  ![스크린샷 2021-04-17 오후 1 44 47](https://user-images.githubusercontent.com/70195733/115102008-6640ff80-9f83-11eb-8f23-989bfc48ef39.png)
- 변형
  - 각 준비 큐마다 시간 할당량을 다르게 배정
    - 프로세스 특성에 맞는 형태로 시스템 운영 가능
  - 입출력 위주 프로세스들을 상위 단계의 큐로 이동, 우선 순위 높임
    - 프로세스가 block될 때 상위의 준비 큐로 진입하게 함
    - 시스템 전체의 평균 응답 시간 줄임, 입출력 작업 분산 시킴
  - 대기 시간이 지정된 시간을 초과한 프로세스들을 상위 큐로 이동
    - aging 기법
- Parameters for MFQ scheduling
  - Queue의 수
  - Queue별 스케줄링 알고리즘
  - 우선 순위 조정 기준
  - 최초 Queue 배정 방법