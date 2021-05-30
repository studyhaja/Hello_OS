# Hybrid paging/segmentation system
## 1. 개요
- Paging + Segmentation의 장점 결합
- 프로그램 분할 방법
  - 1 . 논리 단위의 segment로 분할
  - 2 . 각 segment를 고정된 크기의 page들로 분할
- page 단위로 메모리에 적재
<img width="709" alt="스크린샷 2021-05-30 오후 3 10 44" src="https://user-images.githubusercontent.com/70195733/120094079-388dcf80-c159-11eb-9e2a-acc1e39ff486.png">

## 2. Address mapping
- Virtual address: v = (s, p, d)
  - s: segment number
  - p: page number
  - d: offset in a page
- SMT와 PMT 모두 사용
  - 각 프로세스마다 하나의 SMT
  - 각 segment마다 하나의 PMT
- Address mapping
  - Direct, associated 등
- 메모리 관리
  - FPM과 유사

### 2-1 SMT
<img width="722" alt="스크린샷 2021-05-30 오후 3 14 32" src="https://user-images.githubusercontent.com/70195733/120094162-c7025100-c159-11eb-8491-50fb5d724ad9.png">

### 2-2 PMT
<img width="822" alt="스크린샷 2021-05-30 오후 3 15 16" src="https://user-images.githubusercontent.com/70195733/120094177-dda8a800-c159-11eb-8941-a586255c916d.png">

### 2-3 address mapping table 구조
<img width="827" alt="스크린샷 2021-05-30 오후 3 15 36" src="https://user-images.githubusercontent.com/70195733/120094202-f618c280-c159-11eb-89a0-665ae9b4d07b.png">

### 2-4 Direct address mapping
<img width="834" alt="스크린샷 2021-05-30 오후 3 16 44" src="https://user-images.githubusercontent.com/70195733/120094228-282a2480-c15a-11eb-9252-126839037ac8.png">
- 메모리 접근 3번 하는 단점이 있다.
- 이 단점을 TLB써서 극복하기도 한다.

## 3. Summary
- 논리적 분할(segment)과 고정 크기 분할(page)을 결합
  - page sharing/protection이 쉽다
  - 메모리 할당/관리 overhead가 작다.
  - external fragmentation (o)
  - internal fragmentation (x)
- 전체 테이블의 수 증가
  - 메모리 소모가 큼
  - Address mapping 과정 복잡
- Direct mapping의 경우, 메모리 접근이 3배
  - 성능 저하될 수 있음