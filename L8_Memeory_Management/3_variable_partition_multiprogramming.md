### Remind
Fixed partition multiprogramming에서는 internal/external fragmentation문제로 자원 낭비가 발생할 수 있다.

## Variable Partition Multiprogramming
- 초기에는 전체가 하나의 영역
- 프로세스를 처리하는 과정에서 메모리 공간이 동적으로 분할
- No internal fragmentation

### VPM Example
- Memory Space: 120MB
- 최초 상태
![](https://images.velog.io/images/langssi/post/e8345a0f-c10d-47c4-ae10-a5f79d320b06/image.png)
- Process A enters
![](https://images.velog.io/images/langssi/post/3a074bad-b18b-4470-90a1-318b95e79626/image.png)
- Process B enters
![](https://images.velog.io/images/langssi/post/e795aacb-570b-4e7e-8d9c-b127861d9e23/image.png)
- Processs C enters
![](https://images.velog.io/images/langssi/post/fc08c7fb-ad66-4b3e-a795-f0b14e1d7bd2/image.png)
- Process D enters
![](https://images.velog.io/images/langssi/post/bb4f9c3c-20a7-4122-8015-8c939c026f2a/image.png)
- Process B exits
![](https://images.velog.io/images/langssi/post/83fcb9f8-c9ad-4be3-adbb-9013b979c7b9/image.png)
- Process E enters
![](https://images.velog.io/images/langssi/post/f5f2bb36-d7bd-4ca9-a252-bb8b0ac4d61f/image.png)
- Process D exits
![](https://images.velog.io/images/langssi/post/274d16f2-1d8e-4283-8e9b-b5317270d93e/image.png)

### 어디에 배치 할 것인가?
- Process P enters
![](https://images.velog.io/images/langssi/post/e94ba171-376a-4079-955f-234d0008dac2/image.png)
---
## 배치 전략(Placement strategies)
### First-fit(최초 적합)
- 처음 만나는 알맞은 공간에 넣어줌
- 충분한 크기를 가진 첫번째 partition을 선택
- Simple and low overhead
- 공간 활용률이 떨어질 수 있음
  - 남는 공간이 너무 적거나 너무 크면 비효율적
### Beet-fit(최적 적합)
- Process가 들어갈 수 있는 partition 중 가장 작은 곳 선택
- 탐색 시간이 오래 걸림 -> overhead가 크다.
  - 모든 partition을 살펴봐야 함
- 크기가 큰 partition을 유지할 수 있음
- 작은 크기의 partition이 많이 발생
  - 활용하기 너무 작음(활용 가능성이 적다)
### Worst-fit(최악 적합)
- Process가 들어갈 수 있는 partition 중 가장 큰 곳 선택
- 탐색 시간이 오래걸림
  - 모든 partition을 살펴봐야 함
- 작은 크기의 partition 발생을 줄일 수 있음
- 큰 프로세스에게 필요한 큰 크기의 partition 확보가 어려움
### Next-fit(순차 최초 적합)
- 최초 적합 전략과 유사
- State table에서 마지막으로 탐색한 위치부터 탐색
- 메모리 영역의 사용 빈도 균등화
- Low overhead
---
### 어디에 배치 할 것인가?
- Process P enters 
![](https://images.velog.io/images/langssi/post/31e99666-8cda-4b38-8f77-f68d4c6e0ed8/image.png)
=> External fragmentation issue 발생

## Coalescing Holes(공간 통합)
- 인접한 빈 영역을 하나의 partion으로 통합
![](https://images.velog.io/images/langssi/post/2c761c61-3d03-4d66-966a-bae0079f3858/image.png)
  - Process가 memory를 release하고 나가면 수행
  - Low overhead
  - C가 나가면 P가 들어갈 수 있게 됨
  
## Storage Compaction
![](https://images.velog.io/images/langssi/post/829ad346-b399-419c-985f-bdf41c1eb3bf/image.png)
- 모든 빈 공간을 하나로 통합
  - 공간을 확보하기 위해 프로세스를 멈춰야함 -> high overhead
- 프로세스 처리에 필요한 적재 공간 확보가 필요할때 수행
- High overhead
  - 모든 process 재배치(Process 중지)
  - 많은 시스템 자원을 소비
  - 자주 해줄 수 없고 가끔씩 해야한다.
---
### 요약
- Uni-programming
  - Simple
  - Fragmentation problem
- Fixted partition multi-programming(FPM)
- Variable partition multi-programming(VPM)
  - Placemenmt strategies
    - First-fit, Best-fit, Worst-fit, Next-fit
  - External fragmentation issue
    - Coalescing holes
    - Statage compaction
    
    
### Q. 운영체제가 알아서 해주는데 왜 공부해야하지?
- 동적 할당 -> expensive => 많이 호출하면 프로그램이 느려짐
  - new/malloc 호출 시 system call로부터 os에게 메모리를 받아옴
- Memeory poll 사용 
  - OS에게 한번에 필요한 공간을 받아 온 후 메모리가 필요할때마다 OS까지 가지 않고 포인터를 할당하면 금방 처리 가능
  => memory pool에서 memory allocation 방법 활용하여 메모리 관리
  - 성능 이슈 해결 가능
