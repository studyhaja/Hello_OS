## Memory Management
- Page와 같은 크기로 미리 분할하여 관리/사용
  - Page frame
  - FPM 기법과 유사
- Frame table
  - Page frame당 하나의 entry
  - 구성
    - Allocated/available field
    - PID field
    - Link field: For free list(사용가능한 fp들을 연결)
    - AV: Free list header(free list의 시작점)
### Frame Table
![](https://images.velog.io/images/langssi/post/33a51696-a713-4fb5-be09-b2be0d415b1b/image.png)
- PID: 누가 가져갔느냐
- AV: 가장 처음으로 비어있는 entry 지칭
- link: 내 다음에 누가 비어있는지 기록(빈 entry에 대한 linked list를 만듬)

## Page Sharing
- 여러 프로세스가 특정 page를 공유 가능
  - Non-continous allocation이므로 가능
### 공유 가능 page
- Procedure(function) pages
  - Pure code(reenter code)를 담고 있는 page
- Data page
  - Read-only data
  - Read-write data
     - ME 발생 가능성 -> 병행성(concurrency)제어 기법 관리하에서만 가능
### Example
- Editor 프로그램을 3명이 사용하는 경우
![](https://images.velog.io/images/langssi/post/9caf8759-d306-4518-9eaa-4313a642caac/image.png)
- 사용하는 데이터만 따로 저장됨

### Data page sharing
![](https://images.velog.io/images/langssi/post/af42ada3-3b6c-4020-bfd0-f76514f72c3d/image.png)
- 같은 page frame number를 참조하면 됨

### Procedure page sharing
![](https://images.velog.io/images/langssi/post/beb47879-212d-4722-ab6d-cda9adefa8f8/image.png)
- P1
  - k1: Branch(k1, d)
- P2
  - k2: Branch(k2, d)
  
=> 같은 메모리 주소임에도 불구하고 Branch(k1, d), Branch(k2, d)로 각각 부르는 주소가 달라짐. P2에서 주황 메모리 위치를 기대하여 Branch(K1, d)를 참조하면 완전히 다른 곳을 참조하게 됨
#### Problem
  - 모두 같은 주소지만 부르는 주소가 달라져 다른 프로세스에서 엉뚱한 곳으로 갈 수 있음

#### Solution
  ![](https://images.velog.io/images/langssi/post/000c7a13-4379-4c6c-84eb-31fd02a03f6a/image.png)
  - 프로세스들이 shared page에 대한 정보를 PMT의 같은 entry에 저장하도록 함(부르는 이름 통일)
  
## Page Protection
- 여러 프로세스가 page를 공유할 때(공유: 보안문제 발생 가능)
  - Protection bit 사용


![](https://images.velog.io/images/langssi/post/ab2320a2-c1ce-48eb-a147-dc0220dfe5bb/image.png)
- 공유되는 페이지에 대한 접근 권한을 적어둠

## Summary
- 프로그램을 고정된 크기의 block으로 분할(page), 메모리를 block size로 미리 분할(page frame)
  - 외부 단편화 문제 없음
  - 메모리 통합/압축 불필요
  - 프로그램의 논리적 구조 고려하지 않음 
    - Page sharing/protection이 복잡
- 필요한 page만 page frame에 적재하여 사용
  - 메모리의 효율적 활용
- Page mapping overhead
  - 메모리 공간 및 추가적인 메모리 접근이 필요
  - 전용 HW 활용으로 해결 가능
    - 하드웨어 비용 증가 -> Hybrid Address Mapping 사용
  
