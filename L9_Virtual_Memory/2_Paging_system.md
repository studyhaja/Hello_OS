# Paging system
- 프로그램을 같은 크기의 블록으로 분할하는데, paging system에서는 이 블록을 page라고 부른다.

#### Terminologies
- Page
  - ***프로그램***의 분할된 block
- Page frame
  - ***메모리***의 분할 영역
  - Page와 같은 크기로 분할
<img width="806" alt="스크린샷 2021-05-23 오후 2 49 24" src="https://user-images.githubusercontent.com/70195733/119249750-1551a600-bbd6-11eb-98c1-68f4f8f57e6b.png">

#### 특징
- 논리적 분할이 아니다.
- 크기에 따른 분할이다.
- page 공유 및 보호 과정이 Segmentation에 비해 복잡하다.
- 예를 들자면 segmentation은 함수 단위로 관리해서, 관리가 쉬운데, paging system은 크기 단위로 자르기 때문에 관리가 복잡함
- Simple, Efficient (Segmentation과 비교했을 때)
- No external fragmentation
- Internal fragmentation 발생 가능
<img width="833" alt="스크린샷 2021-05-23 오후 2 53 29" src="https://user-images.githubusercontent.com/70195733/119249813-b2144380-bbd6-11eb-8b64-3b843c67a021.png">

### Address Mapping
- Virtual address: v = (p,d)
  - p: page number
  - d: displacement(offset)
- Address mapping
  - PMT(Page Map Table) 사용
- Address mapping mechanism
  - Direct mapping(직접 사상)
  - Associative mapping(연관 사상)
    - TLB(Translation Look-aside Buffer)
  - Hybrid direct/associative mapping

### PMT(Page Map Table)
- page number: 페이지 번호
- residence bit: 메모리 적재 여부(0/1)
- secondary storage address: 모든 페이지는 swap device에 저장됨. swap device 어디에 저장됐는지에 대한 정보
- page frame number: 메모리 어디에 올라갔는지에 대한 정보
<img width="766" alt="스크린샷 2021-05-23 오후 2 59 29" src="https://user-images.githubusercontent.com/70195733/119249914-834a9d00-bbd7-11eb-9963-b4857a06e25d.png">

### Address Mapping - Direct mapping
- Block mapping과 유사
- 가정
  - PMT를 커널 안에 저장
  - PMT entry size = entrySize(PMT row 하나를 EntrySize라 지칭하겠다.)
  - Page size = pageSize

![스크린샷 2021-05-23 오후 8 15 12](https://user-images.githubusercontent.com/70195733/119258193-a12df700-bc03-11eb-87ee-05e17cf4672b.png)
#### Direct mapping 기본 flow
1. 해당 프로세스의 PMT가 저장되어 있는 주소 b에 접근
2. 해당 PMT에서 page p에 대한 entry 찾음 <br>- p의 entry 위치 = b + p * entrySize
3. 찾아진 entry의 존재 비트 검사 
<br> 3-1. Residence bit = 0 인 경우(page fault), swap device에서 해당 page를 메모리로 적재. PMT를 갱신한 후 3-2단계 수행
<br> 3-2. Residence bit = 1인 경우, 해당 entry page frame 번호 p'를 확인
4. p'와 가상 주소의 변위 d를 사용하여 실제 주소 r 형성
<br> r = p' * pageSize + d
5. 실제 주소 r로 주기억장치에 접근

#### Direct mapping 정리
- 문제점
  - 메모리 접근 횟수가 2배
    - 성능 저하(performance degradation)
  - PMT를 위한 메모리 공간 필요
- 해결방안
  - Associative mapping(TLB)
  - PMT를 위한 전용 기억장치(공간) 사용
    - Dedicated register or cache memory
  - Hierarchical paging
  - Hashed page table
  - Inverted page table
  

### Address Mapping - Associative mapping
- TLB(Translation Look-aside Buffer)에 PMT 적재
  - Associative high-speed memory
- PMT를 병렬 탐색
- Low overhead, high speed
