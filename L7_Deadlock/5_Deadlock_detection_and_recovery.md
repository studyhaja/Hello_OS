# Deadlock detection and deadlock recovery methods(교착상태 탐지 및 복구)

## Deadlock Detection
- Deadlock 방지를 위한 사전 작업을 하지 않음(발생하면 그때 가서 해결하자!)
  - Deadlock 발생 가능함!
- 주기적으로 deadlock 발생 확인
  - 시스템이 deadlock 상태인가?
  - 어떤 프로세스가 deadlock 상태인가?
- resource Allocation Graph(RAG) 사용

#### Resource Allocation Graph(RAG)
- Deadlock 검출을 위해 사용
- Directed, bipartite Graph
  - bi 두개, partite나누다 -> 두개로 나누다.
  - Process(사진상 U)와 Resource(사진상 V)두 개로 나눔
![스크린샷 2021-05-01 오후 9 13 22](https://user-images.githubusercontent.com/70195733/116782077-148b8f80-aac2-11eb-834c-5d53b59ec5df.png)
![스크린샷 2021-05-01 오후 9 13 38](https://user-images.githubusercontent.com/70195733/116782084-21a87e80-aac2-11eb-9b58-b516294852c9.png)
- G = (N, E)
  - G는 그래프, N은 노드, E는 edge
- N = {Np, Nr}
  - 노드는 프로세스 노드와 리소스 노드의 집합이다!
  - {}는 집합을 의미
  - Np는 프로세스 노드
  - Nr은 리소스 노드

![스크린샷 2021-05-01 오후 9 14 45](https://user-images.githubusercontent.com/70195733/116782158-8237bb80-aac2-11eb-9f0b-43534771105c.png)
- e 는 edge
- P -> R 이면 자원 요청
- R -> P 이면 자원 할당
![스크린샷 2021-05-01 오후 9 18 23](https://user-images.githubusercontent.com/70195733/116782224-cc20a180-aac2-11eb-8733-cf9c3782d185.png)
![스크린샷 2021-05-01 오후 9 19 25](https://user-images.githubusercontent.com/70195733/116782245-ece8f700-aac2-11eb-89e6-ac1d435293b2.png)

### Graph reduction
![스크린샷 2021-05-01 오후 9 38 32](https://user-images.githubusercontent.com/70195733/116782697-a0eb8180-aac5-11eb-8219-5474bc8d3ebd.png)
![스크린샷 2021-05-01 오후 9 41 19](https://user-images.githubusercontent.com/70195733/116782769-fb84dd80-aac5-11eb-8116-a982cddb236a.png)
![스크린샷 2021-05-01 오후 9 42 18](https://user-images.githubusercontent.com/70195733/116782789-1eaf8d00-aac6-11eb-97ca-71e4ddf9ae13.png)
![스크린샷 2021-05-01 오후 9 42 18](https://user-images.githubusercontent.com/70195733/116782805-3b4bc500-aac6-11eb-92e0-115251593edd.png)
![스크린샷 2021-05-02 오후 8 52 14](https://user-images.githubusercontent.com/70195733/116812178-51ba5500-ab88-11eb-89d0-d41afa907906.png)
![스크린샷 2021-05-01 오후 9 43 58](https://user-images.githubusercontent.com/70195733/116782832-59b1c080-aac6-11eb-9830-6f81891d1633.png)

![스크린샷 2021-05-01 오후 9 44 39](https://user-images.githubusercontent.com/70195733/116782845-74843500-aac6-11eb-8bb8-573f4e8753ff.png)
![스크린샷 2021-05-01 오후 9 45 40](https://user-images.githubusercontent.com/70195733/116782874-9978a800-aac6-11eb-821a-48422c670a95.png)

## Deadlock Recovery
- deadlock을 검출한 후 해결하는 과정
### Deadlock recovery methods
- process termination
  - deadlock 상태에 있는 프로세스를 종료시킴
  - 강제 종료된 프로세스는 이후 재시작 됨
- Resource preemption
  - deadlock 상태 해결 위해 선점할 자원 선택
  - 선정된 자원을 가지고 있는 프로세스에서 자원을 빼앗음
    - 자원을 빼앗긴 프로세스는 강제종료 됨.

###  process termination
- deadlock 상태인 프로세스 중 일부 종료
- 누구를 종료시킬지 선택해야 함(termination cost model)
#### termination cost model
- 종료 시킬 deadlock 상태의 프로세스 선택
- termination cost
  - 우선순위 / Process priority
  - 종류 / Process type
  - 총 수행 시간 / Accumulated execution time of the process
  - 남은 수행 시간 / Remaining time of the process
  - 종료 비용 / Accounting cost
  - Etc.

- 1) Lowest-termination cost process first
  - Simple
  - Low overhead
  - 불필요한 프로세스들이 종료될 가능성이 높음
- 2) Minimum cost recovery
  - 최소 비용으로 deadlock 상태를 해소할 수 있는 process 선택
    - 모든 경우의 수를 고려해야 함
  - Complex
  - High overhead
    - O(2k승) -> k개의 프로세스가 있으면 경우의 수가 2의 k승

### Resource preemption
- Deadlock 상태 해결을 위해 선점할 자원 선택
- 해당 자원을 가지고 있는 프로세스를 종료시킴
  - Deadlock 상태가 아닌 프로세스가 종료될 수도 있음
  - 해당 프로세스는 이후 재시작 됨
#### 선점할 자원 선택
- Preemption cost model이 필요(선점 기준)
- Minimum cost recovery method 사용
  - O(r)
  
### Checkpoint-restart method
- 프로세스의 수행 중 특정 지점(checkpoint)마다 context를 저장
- Rollback을 위해 사용
  - 프로세스 강제 종료 후, 가장 최근의 checkpoint에서 재시작
![스크린샷 2021-05-02 오후 8 47 57](https://user-images.githubusercontent.com/70195733/116812075-b1643080-ab87-11eb-81fa-04247c7270e6.png)
