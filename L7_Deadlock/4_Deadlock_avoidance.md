# Deadlock avoidance method(교착상태 회피)
- 시스템의 상태를 계속 감시
- 시스템이 deadlock 상태가 될 가능성이 있는 자원 할당 요청 보류
- 시스템을 항상 safe state로 유지!

#### safe state
- 모든 프로세스가 정상적 종료 가능한 상태
- safe sequence가 존재(safe sequence가 존재하면 safe state임.)
  - Deadlock 상태가 되지 않을 수 있음을 보장
#### unsafe state
- Deadlock 상태가 될 가능성이 있음
- 반드시 발생한다는 의미는 아님

#### 가정
- 프로세스의 수가 고정됨
- 자원의 종류와 수가 고정됨
- 프로세스가 요구하는 자원 및 최대 수량을 알고 있음
- 프로세스는 자원을 사용 후 반드시 반납한다.
-> 비현실적(not practical)

#### Dijkstra's algorithm
  - Banker's algorithm
#### Harbermanss's algorithm

## Dijkstra's banker's algorithm
- Deadlock avoidance를 위한 간단한 이론적 기법
- 가정
  - 한 종류(resource type)의 자원이 여러 개(unit)
  - 시스템을 항상 safe state로 유지

#### safe state 예시 
- 자원 종류 1개(R), 자원 10개, 프로세스 3개
![스크린샷 2021-05-01 오후 8 43 25](https://user-images.githubusercontent.com/70195733/116781447-e4da8880-aabd-11eb-8f88-2a6332f41a14.png)

#### unsafe state 예시
![스크린샷 2021-05-01 오후 8 43 58](https://user-images.githubusercontent.com/70195733/116781468-0471b100-aabe-11eb-8173-cbea037f2b16.png)

### bankers algorithm 해보기
- 기존 흐름: 자원 요청이 들어오면, 요청받은 자원을 줬을 때 safe state가 유지 되는지 미리 simulation돌려보고 된다면 자원을 할당해줌, 안되면 Reject
#### accept
![스크린샷 2021-05-01 오후 8 56 44](https://user-images.githubusercontent.com/70195733/116781726-c6758c80-aabf-11eb-9c42-7327974b29eb.png)
#### reject
![스크린샷 2021-05-01 오후 8 56 51](https://user-images.githubusercontent.com/70195733/116781731-caa1aa00-aabf-11eb-9222-bcd991b995cf.png)


## Harbermanss's algorithm
![스크린샷 2021-05-01 오후 9 00 04](https://user-images.githubusercontent.com/70195733/116781803-5b788580-aac0-11eb-9016-efc3d9bab274.png)
![스크린샷 2021-05-01 오후 9 00 10](https://user-images.githubusercontent.com/70195733/116781807-603d3980-aac0-11eb-9e01-5e6cc6d7eda1.png)
![스크린샷 2021-05-01 오후 9 00 58](https://user-images.githubusercontent.com/70195733/116781809-60d5d000-aac0-11eb-9b66-868b0b8e1dff.png)
![스크린샷 2021-05-01 오후 9 01 02](https://user-images.githubusercontent.com/70195733/116781810-616e6680-aac0-11eb-9c38-10421aed2d26.png)

### Deadlock avoidance 정리
- Deadlock의 발생 막을 수있음
- High overhead
  - 항상 시스템 감시해야 함
- Low resource utilization
  - safe state 유지를 위해 사용 되지 않는 자원이 존재
- Not practical
  - 가정
    - 프로세스 수, 자원 수가 고정
    - 필요한 최대 자원 수를 알고 있음

