## 2. 스케줄링 기준(Criteria) 및 단계
### 1) 개요
: 스케줄링 기법이 고려하는 항목들을 살펴보는 챕터
- 프로세스 특성
  - I/O -bounded or compute-bounded
- 시스템 특성
  - batch system or interactive system
- 프로세스의 긴급성(urgency)
  - Hard, soft, non real time system
- 프로세스 우선순위(priority)
- 프로세스 총 실행 시간(total service time)
- 등등.....

### 2) CPU burst vs I/O burst
- 프로세스 수행은 CPU 사용 + I/O 대기로 이루어진다.
- cpu작업 -> I/O 대기 -> cpu 작업 -> I/O대기 ...무한반복
- CPU burst란?
  - CPU 사용 단계
- I/O burst란?
  - I/O 대기 단계
- Burst time은 스케줄링의 중요한 기준 중 하나이다.

### 3) 스케줄링의 단계(Level)
- 스케줄링 단계란 발생하는 빈도 및 할당 자원에 따른 구분으로 총 3가지로 나뉜다.
  - Long-term scheduling
    - Job scheduling
  - Mid-term scheduling
    - Memory allocation
  - Short-term scheduling 
    - Process scheduling

#### Long-term scheduling
- Job scheduling이다.
  - 시스템에 제출할(kernel에 등록할) 작업(Job) 결정
    - Admission scheduling, High-level scheduling
- 다중 프로그래밍 정도(degree) 결정
  - 시스템 내에 프로세스 수 조절
- I/O-bounded와 compute-bounded프로세스들을 잘 섞어서 선택해야 함.
  - 이유는? 둘중 하나에 작업이 너무 몰리면 나머지 하나는 너무 놀게됨
- 시분할 시스템에서는 모든 작업을 시스템에 등록하기 때문에 long-term 스케줄링이 별로 안중요하다.
![스크린샷 2021-04-16 오후 10 20 34](https://user-images.githubusercontent.com/70195733/115030373-fd657300-9f01-11eb-8eff-be553d835760.png)
#### Mid-term scheduling
- 메모리 할당 결정(memory allocation)
  - Intermediate-level scheduling
  - Swapping (swap-in/swap-out)
![스크린샷 2021-04-16 오후 10 21 39](https://user-images.githubusercontent.com/70195733/115030510-2128b900-9f02-11eb-8cab-f4c40aa7ba04.png)
#### Short-term scheduling 
- Process scheduling
  - Low-level scheduling
  - Processor를 할당할 process를 결정
    - Processor scheduler, dispatcher
- 가장 빈번하게 발생
  - Interrupt, block(I/O), time-out, Etc.
  - 매우 빨라야 한다.
  ![스크린샷 2021-04-16 오후 10 22 58](https://user-images.githubusercontent.com/70195733/115030674-50d7c100-9f02-11eb-8b61-8be494645902.png)
![스크린샷 2021-04-16 오후 10 23 27](https://user-images.githubusercontent.com/70195733/115030736-6351fa80-9f02-11eb-8092-a2cb3889726d.png)