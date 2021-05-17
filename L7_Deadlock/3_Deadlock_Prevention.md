### Remind
- Deadlock 발생 필요조건
  - Exclusive use of resorces
  - Non-preemptible resources
  - Hold and wait
  - Circular wait
## Deadlock 해결 조건
- Deadlock Prevention Methods ✔
  - 교착상태 예방
- Deadlock Avoidance Method
  - 교착상태 회피
- Deadlock Detection and Deadlock Recovery Methods
  - 교착상태 탐지 및 복구
  
## Deadlock Prevention
### 4개의 deadlock 발생 필요 조건 중 하나를 제거
- Exclusive use of resources
- Non-preemptible resources
- Hold and wait(Partial allocation)
- Circular wait

=> Deadlock이 절대 발생하지 않음

### 모든 자원을 공유 허용
- Exclusive use of resources 조건 제거
- 현실적으로 불가능

### 모든 자원에 대해 선점 허용
- Non-preemptible resources 조건 제거
- 현실적으로 불가능
- 유사한 방법
  - 프로세스가 할당 받을 수 없는 자원(다른 프로세서가 사용중)을 요청한 경우, 기존에 가지고 있던 자원을 모두 반납하고 작업 취소
    - 이후 처음(또는 check-point)부터 다시 시작
  - 심각한 자원 낭비 발생 -> 비현실적
  
### 필요 자원 한번에 모두 할당(Total Allocation)
- Hold and wait 조건 제거
- 자원 낭비 발생
  - 필요하지 않은 순간에도 가지고 있음(잠깐 쓰이는 자원도 계속 가지고 있음)
- 무한 대기 현상 발생 가능

### Cicular wait 조건 제거
- Totally Allocation을 일반화 한 방법
- 자원들에게 순서를 부여
- 프로세스는 순서의 증가 방향으로만 자원 요청 가능
  - r1 1개, r2 1개, r3 세개, r4 2개가 있다고 하면,
  -	p1이 r1, r2, r3, r4를 사용하고 있는 상황에서 p2는 r1을 할당받지 못하면 남은 r3도 요청하지 못함
- 자원 낭비 발생

=> deadlock을 예방하자니 비현실적이거나 자원의 낭비가 발생 -> 다른 방안 탐구 (회피, 탐지 및 복구)**
