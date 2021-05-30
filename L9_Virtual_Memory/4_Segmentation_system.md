# Segmentation System
## 1. 개요
- 프로그램을 논리적 block으로 분할(segment)
  - block의 크기가 다름
  - 예) stack, heap, main procedure, shared lib, Etc.
## 2. 특징
- 메모리를 미리 분할 하지 않음
  - VPM과 유사
- Segment sharing/protection이 용이함
- Address mapping 및 메모리 관리의 overhead가 큼
- No internal fragmentation
  - External fragmentation 발생 가능
<img width="805" alt="스크린샷 2021-05-30 오후 2 54 05" src="https://user-images.githubusercontent.com/70195733/120093712-e51a8200-c156-11eb-80ed-9c8d500d8be9.png">

## 3. Address mapping
- Virtual address:v = (s, d)
  - s: segment number
  - d: displacement in a segment
- Segment Map Table(SMT)
- Address mapping mechanism
  - Paging system과 유사
<img width="749" alt="스크린샷 2021-05-30 오후 2 55 24" src="https://user-images.githubusercontent.com/70195733/120093735-1430f380-c157-11eb-8363-d9dbe6dd3ade.png">
- secondary storage address: swap device에 저장된 주소
- protection bits: 읽기, 쓰기, 실행, 수정 권한 내역
<img width="817" alt="스크린샷 2021-05-30 오후 2 56 41" src="https://user-images.githubusercontent.com/70195733/120093756-42163800-c157-11eb-9877-1f3b01e031b4.png">

### 3-1. address mapping(direct mapping) 순서
- 1 프로세스의 SMT가 저장되어 있는 주소 b에 접근
- 2 SMT에서 segment s의 entry 찾음
  - s의 entry 위치 = b + s * entrySize
- 3 찾아진 Entry에 대해 다음 단계들을 순차적으로 실행
  - (1) 존재 비트가 0인 경우(segment fault), swapt device로부터 해당 segment를 메모리로 적재, SMT를 갱신
  - (2) 변위(d)가 segment길이보다 큰 경우(d > ls), segment overflow exception처리 모듈을 호출
  - (3) 허가되지 않은 연산일 경우 (protection bit field 검사), segment protection exception처리 모듈을 호출
- 4 실제 주소 r 계산 (r = as + d)
- 5 r로 메모리에 접근

## 4. Memory management
- VPM과 유사
  - segment 적재 시, 크기에 맞추어 분할 후 적재
<img width="719" alt="스크린샷 2021-05-30 오후 3 01 14" src="https://user-images.githubusercontent.com/70195733/120093857-e9936a80-c157-11eb-8687-900c99cc3f6b.png">


## 5. Segment sharing/protection
- 논리적으로 분할되어 있어, 공유 및 보호가 용이함
<img width="677" alt="스크린샷 2021-05-30 오후 3 02 20" src="https://user-images.githubusercontent.com/70195733/120093877-0cbe1a00-c158-11eb-89e3-578851e52f23.png">

## 6. Segmentation System - Summary
- 프로그램을 논리 단위로 분할(sgement)
- 메모리를 동적으로 분할
- no internal fragmentation
- Segment sharing/protection 요이
- Paging system 대비 관리 overhead가 큼
- 필요한 segment만 메모리에 적재
  - 메모리 효율적 활용
- segment mapping overhead
  - 메모리 공간 및 추가적인 메모리 접근이 필요
  - 전용 HW 활용으로 해결 가능
  

## 7. Paging vs Segmentation
<img width="800" alt="스크린샷 2021-05-30 오후 3 04 33" src="https://user-images.githubusercontent.com/70195733/120093931-5dce0e00-c158-11eb-903b-db12d4aeb7e4.png">