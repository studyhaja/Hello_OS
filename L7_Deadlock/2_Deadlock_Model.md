## Deadlock 발생의 예
- 2개의 프로세스 (P1, P2)
- 2개의 자원 (R1, R2)
![](https://images.velog.io/images/langssi/post/4dee55df-ecca-4838-abe8-a5028e92009a/image.png)
- 서로가 가진 자원을 요청 => 발생불가능 => deadlock

## Deadlock Model(표현법)
### Graph Model
- Node
  - 프로세스 노드(P1, P2), 자원 노드(R1, R2)
- Edge
  - Rj -> Pi: 자원 Rj이 프로세스 Pi에 할당됨
  - Pi -> Rj: 프로세스 Pi가 자원 Rj을 요청(대기중)
![](https://images.velog.io/images/langssi/post/01c74297-c8e6-4f0f-9f93-73ccfacf016c/image.png)
4번이 생기는 순간(사이클이 생성되는 순간) deadlock 발생

### State Transition Model
- 예제
  - 2개의 프로세스와 A type의 자원 2개(unit) 존재
  - 프로세스는 한번에 자원 하나만 요청/반납 가능
- State
  ![](https://images.velog.io/images/langssi/post/a7bfe7b7-f1fc-479e-a971-8b7bec16f7c9/image.png)
  - 하나의 프로세스에 5개의 state 존재 -> 프로세스가 2개라면 25개 존재
![](https://images.velog.io/images/langssi/post/395910b0-7306-42c5-b045-2b0b60668955/image.png)
  - S[P1][P2]
  - S33 -> P1, P2가 각각 하나를 갖고 하나를 필요로 하는 상황이므로 발생 할 수 없는 상황임

## Deadlock 발생 필요 조건
### 자원의 특성
- Exclusive use of resources
- Non-preemptible Resources
### 프로세스의 특성
- Hold and Wait(Partial Allocation)
  - 자원을 하나 hold하고 다른 자원 요청
- Circular wait

=> 네 가지를 모두 만족해야 deadlock 발생
