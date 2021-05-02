## 3. 스케줄링 정책
- 선점(Preemptive) vs 비선점(Non-preemptive)
- 우선순위(Priority)
###  선점(Preemptive) vs 비선점(Non-preemptive)
#### Non-preemptive scheduling
- 할당 받은 자원을 스스로 반납할 때까지 사용
  - 예) system call  I/O, Etc.
- 장점
  - context switch overhead가 적음
- 단점
  - 잦은 우선순위 역전, 평균 응답 시간 증가
#### Preemptive scheduling
- 다른 작업에 의해 자원을 뺏길 수 있음
  - 예) 할다 ㅇ시간 종료, 우선순위가 높은 프로세스 등장
- context swtich overhead가 큼
- Time-sharing, real-time system에 적합

### Priority
- : 프로세스의 중요도
#### Static priority(정적 우선순위)
- 프로세스 생성시 결정된 우선순위가 계속 유지됨.
- 구현이 쉽고 overhead가 적음
- 시스템 환경 변화에 대한 대응이 어려움
#### Dynamic priority(동적 우선순위)
- 프로세스의 상태 변화에 따라 priority 변경
- 구현이 복잡, priority 재계산 overhead가 큼
- 시스템 환경 변화에 유연한 대응 가능.

## 요약
![스크린샷 2021-04-16 오후 10 31 22](https://user-images.githubusercontent.com/70195733/115031762-7f09d080-9f03-11eb-8141-2810ae67e077.png)