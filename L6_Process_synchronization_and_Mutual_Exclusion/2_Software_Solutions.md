## Mutual Exclusion Solutions
### SW solutions
- Dekker’s algorithm (Peterson’s algorithm)
- Dijkstra’s algorithm, Knuth’s algorithm, Eisenberg and McGuire’s algorithm, Lamport’s algorithm
### HW solution
- TestAndSet (TAS) instruction
### OS supported SW solution
- Spinlock
- Semaphore
- Eventcount/sequencer
### Language-Level solution
- Monitor

## Dekker's Algorithm
- Two process ME을 보장하는 최초의 알고리즘
- turn과 flag를 둘다 씀
![](https://images.velog.io/images/langssi/post/d3825ff3-9e46-458b-86d1-18776cb4c74e/image.png)



깃발을 들고 들어감 -> 만약 상대가 깃발을 안들고 있으면 cs로 바로 진입, 만약 상대도 깃발을 들고 있으면 turn을 확인 -> 자신의 turn이 아니라면 대기, turn이 오면 cs 진입

### 문제 해결 확인
- turn0인채로 p0가 죽어버렸을때(맨 위의 repeat 부분에서 죽었다고 가정)
  - p1은 깃발을 들고 p0의 깃발을 확인했을때 내려가있으므로 cs 진입 가능 -> progress 조건 위배하지 않음
- 둘다 깃발을 들고 있어도 턴을 한번 더 확인 -> ME, progress, BW 문제 해결됨

## Peterson's Algorithm
- Dekker's algorithm보다 간단하게 구현
- 양보하는 점이 다름
![](https://images.velog.io/images/langssi/post/36b49046-b0f2-4a28-867a-0916d597a569/image.png)

## N-Process Mutual Exclusion
### 다익스트라(Dijkstra)
- 최초로 프로세스 n개의 상호배제 문제를 소프트웨어적으로 해결
- 실행시간이 가장 짧은 프로세스에 프로세서를 할당하는 세마포 방법, 가장 짧은 평균 대기시간 제공

## Dijkstra's Algorithm
![](https://images.velog.io/images/langssi/post/e427ca35-2b25-4aca-899a-631c5c3f6d3e/image.png)
3개의 상태를가진다
1. 들어올 생각 없음
2. 들어올 생각 있음
3. 진입하기 직전

![](https://images.velog.io/images/langssi/post/dd05e237-95c5-4b03-9c73-9ba76dca188f/image.png)
### Step1
- flag를 want-in 상태로 바꿈
- 내 turn이 아니면 기다리고 턴이었던 프로세스가 idle 상태로 바뀌면 turn을 자신으로 바꿈
- 다른 프로세스들도 turn을 계속 뺏고 있기 때문에 계속 반복됨
### Step2
- 여러 프로세스가 2단계 진입 가능
- flag를 in-CS로 변경
- j가 n보다 작을때까지 돌며, in-CS 상태에 자신이 아닌 프로세스가 있다면 for문을 빠져나감
  - j < n이면 처음으로 돌아감
- 만약 자신만 있다면 n까지 돌게되고 j==n이 됨
  - cs에 들어갈 수 있음(cs 상태가 오직 자신뿐이라면 cs에 진입) -> ME 해결

## SW solution들의 문제점
- 속도가 느림(뺑뺑 도는 느낌이 있다)
- 구현이 복잡함
- ME primitive 실행 중에 preemption이 될 수 있음(위에서는 일어나지 않는다고 가정하고 진행했음)
  - 공유 데이터 수정 중은 interrupt를 억제함으로서 해결 가능
    - overhead 발생
- Busy Waiting(기다리는데에 바쁨 - 뺑뺑 돌면서 기다림)
  - Inefficient
