## Virtual Memory Management
### 가상 메모리(기억장치)
- Non-continuous allocation
  - 사용자 프로그램을 block으로 분할하여 적재/실행
- Paging/Segmentation system

### 가상 메모리 관리의 목적
- 가상 메모리 시스템 성능 최적화
  - Cost model
    - 성능의 지표는 다양하기 때문에 성능 최적화라는 의미는 모호하므로 cost model이 필요하다.
  - 다양한 최적화 기법
  
## Cost Model for virtual Mem. Sys.
### Page fault frequency (발생빈도)
- Page fault: CPU가 보려는 데이터가 Memomoy상에 없는 경우(해당 프로세스는 block 상태로 변경됨)
  - context switch 발생
### Page fault rate(발생률)
### Page fault rate를 최소화 할 수 있도록 전략들을 설계해야 함
- Contenxt switch 및 Kernel 개입을 최소화
- 시스템 성능 향상
## 용어(Paging System)
### Page reference string(d)
- 프로세스의 수행 중 참조한 페이지 번호 순서
- ![](https://images.velog.io/images/langssi/post/2981ff9f-3b07-4fac-bfa7-a5178493738a/image.png)
- 왜 기록을 할까?
  - virtual memory를 효율적으로 사용 -> page fault를 본다. 즉 어떤 페이지를 읽어왔는지에 대한 정보가 필요하다. 효율적인 알고리즘을 설계하기 위해서

### Page fault rate = F(w)
![](https://images.velog.io/images/langssi/post/b17c35c9-f569-42ef-8eaa-7379e27a57e5/image.png)
- `|w|`: 참조했던 페이지의 수

## Hardware Components
### Address translation device(주소 사상 장치)
- 주소 사상(변경)을 효율적으로 수행하기 위해 사용
  - E.g., TLB(associated memories), Dedicated page-table register, Cache memories
### Bit Vectors
- bit들이 array형식으로 있는 것 ex.`{1,0,1,0,0,1}`
- Page 사용 상황에 대한 정보를 기록하는 비트들
- Reference bits(used bit)
  - 참조 비트
  - 해당 페이지 프레임이 참조 되었는가?
- Update bits(modified bits, write bits, dirty bits)
  - 갱신 비트
  - 해당 페이지 프레임에서 갱신이 발생했는가?
  
## Bit Vectiors
![](https://images.velog.io/images/langssi/post/df48345d-3ff0-4095-9586-bbbcd03049ff/image.png)
- 메모리를 효율적으로 사용하기 위해서 PMT로 데이터 프레임에 대한 정보를 관리한다.
  - ex. 새로운 데이터가 들어오는데 누구를 빼고 어디에 넣어줘야할까...
### Reference bit vector
- 메모리에 적재된 각각의 page가 **최근에** 참조되었는지를 표시
  - 페이지를 바꿔야 하는데 누구를 바꾸는 것이 좋을까?를 결정하기 위해 필요한 정보
  ![](https://images.velog.io/images/langssi/post/3a849393-d2b1-43a2-9a08-31e5ef27bbff/image.png)
  - 특정 시점마다 모든 ref bit를 0으로 만들고 그 사이에 참조가 되면 1로 바꿔주므로 최근에 참조된 것을 알 수 있다.
- 운영
  - 1. 프로세스에 의해 참조되면 해당 page의 Ref.bit를 1로 설정
  - 2. 주기적으로 모든 reference bit를 0으로 초기화
- Reference bit를 확인함으로서 최근에 참조된 page들을 확인 가능(locality)

### Update bit vector
- Page가 메모리에 적재된 후, 프로세스에 의해 수정되었는지를 표시
- 주기적 초기화 없음
  - 원본 데이터들은 모두 Swap device에 있고 프로세스는 Memory에 올라간 데이터들을 수정하고 수정 내용은 기록된다. 수정된 데이터는 더이상 프로세스에서 필요하지 않게되어 메모리 밖으로 나올때(update bit이 0으로 초기화) 수정 내용을 swap device에 있는 데이터에 반영한다.
- Update bit = 1
  - 해당 page의 (Main memory상 내용) != (Swap device의 내용)
  - 해당 page에 대한 Write-back(to swap device)이 필요
