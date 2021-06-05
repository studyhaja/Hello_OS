# 교체기법
#### 가상 메모리 성능 향상을 위한 관리 기법들
- Allocation strategies(할당 기법)
- Fetch strategies
- Placement strategies(배치 기법)
- ***Replacement strategies(교체 기법)***
- Cleaning strategies(정리 기법)
- Load control strategies(부하 조절 기법)

## 1. Locality
- 프로세스가 프로그램/데이터의 특정 영역을 집중적으로 참조하는 현상
- 원인
  - Loop structure in program
  - Array, structure등의 데이터 구조
- 공간적 지역성(Spatial locality) 
  - 참조한 영역과 인접한 영역을 참조하는 특성
- 시간적 지역성(Temporal locality)
  - 한 번 참조한 영역을 곧 다시 참조하는 특성
![스크린샷 2021-06-05 오후 8 47 28](https://user-images.githubusercontent.com/60768642/120890680-57033780-c63f-11eb-8ae1-fea7578a2bac.png)
![스크린샷 2021-06-05 오후 8 47 41](https://user-images.githubusercontent.com/60768642/120890684-5a96be80-c63f-11eb-8e63-bd9971054456.png)


## 2. 교체 기법 방법들
### Fixed allocation
- MIN(OPT, B0) algorithm
- Random algorithm
- FIFO(First In First Out) algorithm
- LRU(Least Recently Used) algorithm
- LFU(Least Frequently Used) algorithm
- NUR(Not Used Recently) algorithm
- Clock algorithm
- Second change algorithm
### Variable allocation
- WS(Working Set) algorithm
- PFF(Page Fault Frequency) algorithm
- VMIN(Variable MIN) algorithm


#### 1) MIN(OPT, B0) algorithm
- 1966년 Belady에 의해 제시
- Minimize page fault frequency(proved) -> 페이지 폴트를 최소하 시키는 방법으로 이미 증명이 됨.
  - Optimal solution( 다른 말로 최적의 방법이라고 불림)
- 기법
  - 앞으로 가장 오랫동안 참조되지 않을 page 교체
    - Tie-breaking rule: 동점일 경우, page번호가 가장 큰/작은 페이지 교체
- 실현 붕가능한 기법(Unrealizable)
  - Page reference string을 미리 알고 있어야 함
- 교체 기법의 성능 평가 도구로 사용됨
![스크린샷 2021-06-05 오후 8 58 36](https://user-images.githubusercontent.com/60768642/120890992-160c2280-c641-11eb-837f-88cbe4807fd2.png)
![스크린샷 2021-06-05 오후 9 00 34](https://user-images.githubusercontent.com/60768642/120890995-1a384000-c641-11eb-9be5-4e5fa3523358.png)

#### 2) Random Algorithm
- 무작위로 교체할 page 선택
- Low overhead
- No policy

#### 3) FIFO Algorithm
- 가장 오래된 페이지 교체
- Page가 적재된 시간 기억하고 있어야 함
- 자주 사용되는 page가 교체될 가능성이 높음
  - Locality에 대한 고려가 없음
- FIFO anomaly(Belady's anomaly)
  - FIFO알고리즘의 경우, 더 많은 page frame을 할당 받음에도 불구하고 page fault가 증가하는 경우가 있음
![스크린샷 2021-06-05 오후 9 18 58](https://user-images.githubusercontent.com/60768642/120891449-b5321980-c643-11eb-805e-0463b3db9f01.png)
![스크린샷 2021-06-05 오후 9 19 14](https://user-images.githubusercontent.com/60768642/120891454-b95e3700-c643-11eb-92f8-f9aa01579e12.png)

#### 4) LRU(Least Recently Used) Algorithm
- 가장 오랫동안 참조되지 않음 page를 교체
- page참조시마다 시간을 기록해야 함
- Locality에 기반을 둔 교체 기법
- MIN 알고리즘에 근접한 성능
- 실제로 가장 많이 사용되는 기법
- 단점
  - 참조시 마다 시간을 기록해야 함(Overhead)
    - 간소화된 정보 수집으로 해소 가능(예시: 정확한 시간 대신 순서만 기록)
  - Loop 실행시 필요한 크기보다 작은 수의 page frame이 할당된 경우, page fault수가 급격히 증가함
![스크린샷 2021-06-05 오후 9 22 18](https://user-images.githubusercontent.com/60768642/120891562-39849c80-c644-11eb-8df3-a564d8130855.png)
![스크린샷 2021-06-05 오후 9 22 39](https://user-images.githubusercontent.com/60768642/120891563-3a1d3300-c644-11eb-92c3-1feaa087345f.png)

#### 5) LFU(Least Frequently Used) Algorithm
- 가장 참조 횟수가 적은 Page 교체
  - Tie-breaking rule: LRU, 근데 동점 시 룰은 정하기 나름이다!
- Page 참조시 마다, 참조 횟수를 누적시켜야 함
- Locality 활용
  - LRU 대비 적은 overhead
- 단점
  - 최근 적재된 참조될 가능성인 높은 page가 교체될 가능성이 있음
  - 참조 횟수 누적 overhead
![스크린샷 2021-06-05 오후 10 09 29](https://user-images.githubusercontent.com/60768642/120892797-ee21bc80-c64a-11eb-997d-89e8e06a916a.png)
![스크린샷 2021-06-05 오후 10 10 59](https://user-images.githubusercontent.com/60768642/120892802-f37f0700-c64a-11eb-8779-44c26f26853c.png)

#### 6) NUR(Not Used Recently) Algorithm
<img width="1307" alt="스크린샷 2021-06-05 오후 10 15 09" src="https://user-images.githubusercontent.com/60768642/120892936-8324b580-c64b-11eb-874d-0a8ebdee858d.png">
<img width="1238" alt="스크린샷 2021-06-05 오후 10 16 02" src="https://user-images.githubusercontent.com/60768642/120892959-a7809200-c64b-11eb-9493-e99907e80581.png">

#### 7) Clock Algorithm
- IBM VM/370 OS (무슨 말인지 모르곘다)
- Reference bit 사용함
  - 주기적인 초기화 없음
  - 시계 바늘이 지나가며 초기화 시킴(뒤에 설명 나옴)
- Page frame들을 순차적으로 가리키는 pointer(시계 바늘)를 사용하여 교체될 page 결정
![스크린샷 2021-06-05 오후 10 21 27](https://user-images.githubusercontent.com/60768642/120893114-63da5800-c64c-11eb-9e98-4b25915d2ec7.png)
- Pointer를 돌리면서 교체 page 결정
  - 현재 가리키고 있는 page의 reference bit(r) 확인
  - r = 0인 경우, 교체 page로 결정
  - r = 1인 경우, reference bit 초기화 후 pointer 이동
- 먼저 적재된 page가 교체될 가능성이 높음
  - FIFO와 유사
- Reference bit를 사용하여 교체 페이지 결정
  - LRU(or NUR)과 유사
![스크린샷 2021-06-05 오후 10 23 02](https://user-images.githubusercontent.com/60768642/120893144-9b490480-c64c-11eb-8c4c-4bdb62ecf33f.png)

#### 8) Second Change Algorithm
![스크린샷 2021-06-05 오후 10 24 08](https://user-images.githubusercontent.com/60768642/120893213-085c9a00-c64d-11eb-8c1b-63961e9c3e6e.png)
![스크린샷 2021-06-05 오후 10 24 23](https://user-images.githubusercontent.com/60768642/120893216-0c88b780-c64d-11eb-9870-963230472e14.png)
![스크린샷 2021-06-05 오후 10 26 01](https://user-images.githubusercontent.com/60768642/120893217-0db9e480-c64d-11eb-9631-a5a2dc7746e1.png)
![스크린샷 2021-06-05 오후 10 34 23](https://user-images.githubusercontent.com/60768642/120893413-31c9f580-c64e-11eb-92b1-a59d6915d571.png)
  