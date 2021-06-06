## Software Components
### 가상 메모리 성능 향상을 위한 관리 기법들
- Allocation Strategies(할당 기법)
- Fetch Strategies
- Placement Strategies(배치 기법)
- Replacement Strategies(교체 기법)
- Cleaning Strategies(정리 기법)
- Load Control Strategies(부하 조절 기법)

## Allocation Strategies
### 각 프로세스에 메모리를 얼마만큼 줄 것인가?
- Fixed allocation(고정 할당)
  - 프로세스의 실행동안 고정된 크기의 메모리 할당
  - ex. Paging system
- Variable allocation(가변 할당)
   - 프로세스의 실행동안 할당하는 메모리의 크기가 유동적
   - ex.Segmentation system
### 고려사항
- 프로세스 실행에 필요한 메모리 양을 에측해야 함
- 너무 큰 메모리 할당(Too much allocation)
  - 메모리가 낭비됨
- 너무 적은 메모리 할당(Too small allocation
  - Page fault rage ↑
  - 시스템 성능 저하
  
## Fetch Strategies
*fetch: 어떤 데이터를 가져오는 것(swap device -> memory)
### 특정 page를 메모리에 언제 적재할 것인가?
- Demand fetch(demand paging)
  - 프로세스가 참조하는 페이지들만 적재
  - page fault overhead
- Anticipatory fetch(pre-paging/prefetch)
  - 참조될 가능이 높은 page 예측
  - 가까운 미래에 참조될 가능성이 높은 page를 미리 적재
  - 에측 성공시, page fault overhead가 없음
    - 하지만 예측 실패시에는 overhead가 더 크게 발생(가져다 놓고 새로 가져옴)
  - Prediction overhead(Kernel의 개입), Hit(예상이 얼마나 잘 들어맞는가) ratio에 민감함
### 실제 대부분의 시스템은 Demand fetch 기법 사용
- 일발적으로 준수한 성능을 보여줌
  - But, 성능이 좋은 프로그램을 짜기 위해서 고려할 수 있는 방안임
- Anticipatory fetch
  - Prediction overhead, 잘못된 예측시 자원 낭비가 큼

## Placement Strategies
- Page/segment를 어디에 적재할 것인가?
- Paging system에는 불필요
- Segmentation system에서의 배치 기법
  - First-fit
  - Best-fit
  - Worst-fit
  - Next-fit

## Replacement Strategies
- 새로운 page를 어떤 page와 교체할 것인가?(빈 page frame이 없는 경우)
- Fixed allocation을 위한 교체 기법
  - MIN(OPT, B0) algorithm
  - Random algorithm
  - FIFO(First In First Out) algorithm
  - LRU(Least Recently Used) algorithm
  - LFU(Least Frequently Used) algorithm
  - NUR(Not Used Recently) algorithm
  - Clock algorithm
  - Second chance algorithm
- Variable allocation을 위한 교체 기법
  - VMIN(Variable MIN) algorithm
  - WS(Working Set) algorithm
  - PFF(Page Fault Frequency) algorithm
  
## Cleaning Strategies
### 변경 된 page를 언제 write-back 할 것인가?
- write-back: 변경된 내용을 swap device에 반영(dirty bit를 cleaning)
- Demand cleaning
  - 해당 page가 메모리에서 내려올때 write-back
- Anticipatory cleaning(pre-cleaning)
  - 더이상 변경될 가능성이 없다고 판단 할 때 미리 write-back
  - Page 교체 시 발생하는 write-back 시간 절약
  - Write-back 이후, page 내용이 수정되면, overhead!
  
### 실제 대부분의 시스템은 Demand cleaning 기법 사용
- 일반적으로 준수한 성능을 보여줌
- Anticipatory cleaning
  - Prediction overhead, 잘못된 예측시 자원 낭비가 큼

## Load Control Strategies
*Load control: 부하 조절
### 시스템의 multi-programming degree 조절
- Allocation strategies와 연계 됨
### 적정 수준의 multi-programming degree를 유지해야함
- Plateau(고원) 영역으로 유지
![](https://images.velog.io/images/langssi/post/1d75dbed-c066-498e-b8f2-2de09888afc2/image.png)
- 저부하 상태(Under-loaded)
  - 시스템 자원 낭비, 성능 저하
- 고부하 상태(Over-loaded)
  - 자원에 대한 경쟁 심화, 성능 저하
  - Thrashing(스레싱) 현상 발생
    - 과도한 page fault가 발생하는 현상
