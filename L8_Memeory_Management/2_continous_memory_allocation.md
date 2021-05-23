## Memory Allocation
메모리를 어떻게 프로세스에 할당해주는가?
## Continuous Memory Allocation
-  프로세스(context)를 하나의 연속된 메모리 공간에 할당하는 정책
   - 프로세스, 데이터, 스택 등
### 메모리 구성 정책
- 메모리에 동시에 올라갈 수 있는 프로세스 수
  - Multiprogramming Degree
- 각 프로세스에게 할당되는 메모리 공간 크기
  - 프로세스가 요구하는만큼 줄 수 있는가?
- 메모리 분할 방법
---
## Uni-programming
- Multiprogramming Degree = 1
- 하나의 프로세스만 메모리 상에 존재
- 가장 간단한 메모리 관리 기법
### 문제점
- 프로그램의 크기 > 메모리 크기
  - 프로그램을 잘라서 올린다? 운영체제가 잘라줄 수는 없다 => 프로그래의 역할
- 커널(kernel) 보호
  - 프로그램 올릴 때 커널을 침범해서는 안된다.
- Low system resource utilizatio
  - 프로세스 하나만 올라가므로 남은 공간이 낭비됨
- Low system performance
### 해결법
- Overlay structure

    ![](https://images.velog.io/images/langssi/post/e8a657d6-9482-4a9a-bcdf-eeee981d3fb8/image.png)
  - 메모리에 현재 필요한 영역만 적재
  - 사용자가 프로그램의 흐름 및 자료구조를 모두 알고 있어야 함(무엇이 공통이고 아닌지 알고 있어야 함)
- 경계 레지스터(boundary register) 사용
![](https://images.velog.io/images/langssi/post/0a35ab9b-4170-41fd-a58c-b1f3944a2689/image.png)
  - boundary address를 적어 둠으로서 침범하지 않도록 한다.
- Multi-programming
---
## Multi-programming
### Fixed(static) partition multi-programming(FPM)
- 메모리 공간을 고정된 크기로 분할
  - 미리 분할해 둠


  ![](https://images.velog.io/images/langssi/post/81c3b881-8abc-417b-b1c9-a18f7105c4cf/image.png)
  - 하나의 프로세스를 적당한 공간에 둠
- 각 프로세스는 하나의 partition(분할)에 적재
  - Process : Partition = 1 : 1
- Partiton의 수 = K
  - Multiprogramming degree = K
- 자료 구조의 예
  ![](https://images.velog.io/images/langssi/post/b628814b-7e39-4c1f-8816-8267d1c7d85e/image.png)
- 커널 및 사용자 영역 보호(각 파티션도 침범하면 안됨)
  ![](https://images.velog.io/images/langssi/post/b1c4a4bb-3412-455f-9189-bd19b73d5378/image.png)
## 단편화
### Internal fragmentation
![](https://images.velog.io/images/langssi/post/751ea117-779f-4665-968f-a094fd7fdf39/image.png)
- 내부 단편화
- Partition 크기 > Process 크기
  - 메모리가 낭비 됨
### External fragmentation
![](https://images.velog.io/images/langssi/post/bd0fe9e3-e180-47ba-b35e-1ad6fd9360ba/image.png)
- 외부 단편화
- (남은 메모리 크기 > Process 크기)지만 연속된 공간이 아님
  - 총 44MB가 남아 있지만 각각 다른 방이므로 Process 4가 들어갈 수 없음
  - 메모리가 낭비 됨
### 요약
- 고정된 크기로 메모리 미리 분할
- 메모리 관리가 간편함 -> Low Overhead
- Interanl/External fragmentation -> 시스템 자원이 낭비될 수 있음
