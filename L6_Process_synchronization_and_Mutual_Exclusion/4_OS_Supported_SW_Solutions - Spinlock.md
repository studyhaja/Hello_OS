### Remind
HW solution에서도 Busy waiting 문제는 여전히 발생했다.

# OS supported SW Solution
## Spinlock
- 정수 변수 S
- 초기화, P(), V() 연산으로만 접근 가능
  - 위 연산들은 indivisible(or atomic) 연산
    - OS support(P, V 연산 중에는 preemption을 하지 않을 것을 OS가 보장)
    - 전체가 한 instruction cycle에 수행됨
![](https://images.velog.io/images/langssi/post/4f8a885e-aae9-45a6-9a09-cd7f3647ec3e/image.png)
- S: 물건의 갯수
- P: 물건을 빼가는 것 또는 자물쇠
- V: 물건을 집어 넣는 것 또는 자물쇠를 푸는 것

### ME 문제 해결
![](https://images.velog.io/images/langssi/post/b8d37cf2-bf46-47d5-b321-bc5effff77ac/image.png)
- P, V 연산은 interrupt가 발생하지 않기 때문에 동시에 들어가거나 동시에 못들어가는 상황이 발생하지 않는다.
- p1에서 자물쇠를 잠구고 cs에 있을때(active 1->0) p1은 P에서 계속 대기하게 되고, p0이 물건을 반납(active 0->1)했을때 cs로 진입 가능하다.
## Spinlock의 문제
- 멀티 프로세서 시스템에서만 사용 가능
  - cpu가 하나라면? 
    - p0이 critical section 안에서 중단되면(cpu에서 쫒겨나면) p1이 cpu를 차지하게 되고 p1에서는 P가 계속 실행되는 상황
    - 하지만 P는 atomic하므로 OS에서 중단하지 않기 때문에 p1은 자원을 못받고 p0도 cpu를 할당받을 수 없는, 결국은 둘 다 일을 하지 못하는 상황이 발생함
- Busy Waiting!
  - `while (S<=0)`...
