# Virtual Memory(non-continuous allocation)

## Virtual Storage(Memory)
- ***Non-continuous allocation***
- (참고: continuous aloocation은 연속된 메모리 공간에 프로세스를 올리는 것)
- ***사용자 프로그램을 여러 개의 block으로 분할한다.***
- ***실행 시, 필요한 block들만 메모리에 적재한다.***
  - 나머지 block들은 swap device에 존재함.(swap device를 디스크로 이해하면 됨)

- 기법들
  - paging system
  - Segmentation system
  - Hybrid paging/segmentation system
 

## Address Mapping
- memory allocation을 하면 Address Mapping이 필연적으로 따라온다.

### continuous allocation
- Relative address(상대 주소)
  - 프로그램의 시작 주소를 0으로 가정한 주소
- Relocation(재배치)
  - 메모리 할당 후, 할당된 주소(allocation address)에 따라 상대 주소들을 조정하는 작업
  <img width="1029" alt="스크린샷 2021-05-23 오후 2 29 49" src="https://user-images.githubusercontent.com/70195733/119249422-62804880-bbd3-11eb-92e2-b92b27ccc4be.png">

### Non-continuous allocation
- Virtual address(가상 주소) = relative address
  - logical address (논리 주소)
  - 연속된 메모리 할당을 가정한 주소(프로그래머가 프로그램 어디서부터 어디까지 자를지 고민하지 않고 통으로 짜도 됨)
- Real address(실제 주소) = absolute(physical)
  - 실제 메모리에 적재된 주소

- virtual memory에서 Address mapping이라는 말은 virtual address를 real address로 바꿔주는 것을 의미한다.
<img width="820" alt="스크린샷 2021-05-23 오후 2 35 45" src="https://user-images.githubusercontent.com/70195733/119249530-2d282a80-bbd4-11eb-862b-d67189232f45.png">

### Block Mapping(adress mapping 기법)
- 사용자 프로그램을 block 단위로 분할/관리
  - 각 block에 대한 address mapping 정보 유지
<img width="830" alt="스크린샷 2021-05-23 오후 2 37 04" src="https://user-images.githubusercontent.com/70195733/119249564-6f516c00-bbd4-11eb-82ec-bf889407ed34.png">

#### Block map table(BMT)
- Address mapping 정보 관리
  - Kernel 공간에 프로세스마다 하나의 MBT를 가짐
  
- block number: 블록 번호
- residence bit: 메모리에 올라갔는지 여부(0/1, 1이면 올라가있는 상태)
- real address: 실제 물리 주소
<img width="735" alt="스크린샷 2021-05-23 오후 2 41 03" src="https://user-images.githubusercontent.com/70195733/119249615-ea1a8700-bbd4-11eb-93f1-f5bfbbedcd44.png">

#### Block mapping 순서
1. 프로세스의 BMT 접근
2. BMT에서 block b에 대한 항목(entry)를 찾음
3. Residence bit 검사
  3-1. Residence bit = 0인 경우, swap device에서 해당 블록을 메모리로 가져옴. BMT 업데이트 후 3-2 수행 
  3-2. Residence bit = 1인 경우, BMT에서 b에 대한 readl address 값 a 확인
4. 실제 주소 r 계산(r = a + d)
5. r을 이용하여 메모리에 접근
