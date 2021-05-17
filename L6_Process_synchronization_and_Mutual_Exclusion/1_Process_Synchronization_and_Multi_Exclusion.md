# 프로세스 동기화 & 상호배제
## 동기화(Process Synchronization)
### 다중 프로그래밍 시스템
- 여러개의 프로세스들이 존재
- 프로세스들은 서로 독립적으로 동작(=>동시에 동작)
- 공유 자원 또는 데이터가 있을때, 문제 발생 가능(ex. 한 종이에 동시에 그림을 그린다면 원하는 결과가 나오지 않을 수 있음 -> 대화를 나누어 약속을 정해야한다(=> 동기화))
### 동기화(Synchronization)
- 프로세스들이 서로 동작을 맞추는 것
- 프로세스들이 서로 정보를 공유하는 것
- 즉, 대화하는 행위

## Asynchronous and Concurrent P's
### 비동기적(Asynchronous)
- 프로세스들이 서로에 대해 모름
### 병행적(Concurrent)
- 여러개의 프로세스들이 동시에 시스템에 존재
=> 병행 수행중인 비동기적 프로세스들이 공유 자원에 동시 접근할 때 문제가 발생할 수 있음

## Terminologies
### Shared Data(공유 데이터) or Critical Data
- 여러 프로세스들이 공유하는 데이터
### Critical Section(임계 영역)
- 공유 데이터를 접근하는 코드 영역(code segment)
### Mutual Exclustion(상호 배제)
- 둘 이상의 프로세스가 동시에 critical section에 진입하는 것을 막는 것

## Critical Section
![](https://images.velog.io/images/langssi/post/fe29bb09-2feb-4fcf-8c63-1a1b4ae2f1b8/image.png)
*sdata: hared data

memory에 최종적으로 뭐가 들어가게될까?(기대 => 2)
> 
- 기계어 명령(machine instruction)의 특성
  - Atomicity(원자성), Indivisible(분리불가능)
  - 한 기계어 명령의 실행 도중에 인터럽트 받지 않음
  
### s=s+1에 대한 컴파일러의 번역 결과
![](https://images.velog.io/images/langssi/post/aa5579d5-41cd-4e19-a418-85b169b9ace3/image.png)
1. R(레지스터)의 sdata 값을 읽어와라
2. 1을 더해라
3. sdata를 다시 R에 저장해라
  
메모리 상의 데이터 -> 레지스터에 가져와서 작업 한 뒤 -> 메모리에 저장

그럼 메모리에 최종적으로 저장되는 값은 2일까? 
=> **상황에 따라 다르다!**

1번, 2번, 3번 각각 작업할때는 끼어들 수 있지만 각 번호 사이에는 끼어들 수 있기 때문

preemption(running->ready)가 발생하는 경우 생각
1 이후 preemption 발생 -> pj에서 1실행 -> Rj+1(2번작업) 이후 preemption 발생 -> pi의 2번 실행(0+1 =1) -> 3번 수행 (메모리에 1 적재) -> pj의 3번 실행 -> 메모리에 1 적재
=> 1이 들어가는 경우가 발생할 수 있음
![](https://images.velog.io/images/langssi/post/fec9d85d-3b3a-41b4-8a5a-c5356d0c27cd/image.png)
실행 순서에 따라 결과가 달라지는 것: Race Condition

## Mutual Exclusion(상호 배제)
![](https://images.velog.io/images/langssi/post/96bfde03-79e5-43dd-9b3f-195dc936c4b2/image.png)
pi 1~3을 실행하는 동안 인터럽션이 발생하지 않도록 함

## Mutual Exclusion Methods
### Mutual Exclusion Primitives
*프리미티브: 가장 기본이 되는 연산(기본연산)
- enterCS() primitive
  - Critical Section 진입 전 검사 (누가 있는지 검사)
  - 다른 프로세스가 Critical Sction 안에 있는지 검사
- exitCS() primitive
  - Critical Section을 벗어날 때의 후처리 과정 
  - Critical Sction을 벗어남을 시스템이 알림 (기다리는 애 들어와)
  ![](https://images.velog.io/images/langssi/post/ae4fb81a-2aba-4616-b15f-55e94205d879/image.png)

## Requirements for ME primitives
### Mutual Exclusion(상호배제)
- Critical Sction(CS)에 프로세스가 있으면, 다른 프로세스의 진입을 금지
### Progress(진행)
- CS 안에 있는 프로세스 외에는, 다른 프로세스가 CS에 진입하는 것을 방해하면 안됨(도착하지 않은 프로세스가 들어가려는 프로세스를 방해할 수 없음)
### Bounded Waiting(한정대기)
- 프로세스의 CS 진입은 유한시간 내에 허용되어야 함

## Two Process Mutual Exclusion
### v1
내 턴일때만 들어갈 수 있음
![](https://images.velog.io/images/langssi/post/e1b58d3b-e6e1-410c-a1e7-d2485f738da6/image.png)
*여기서는 `=`:`==`과 동일하게 생각(pseudo code 이므로)

### Progress 조건 위배
- P0이 critical section에 진입 하지 않는 경우
  - p0이 cs에 진입하기 전 죽어버리면 cs는 비어있지만 P1은 영영 들어갈 수 없음
- 한 process가 두번 연속 cs에 진입 불가
  - p0이 turn을 넘기고 다시 돌아왔을때 p1보다 먼저 도착했을때 cs가 비어있어도 들어갈 수 없음

### v2
flag -> 내가 들어갈거면 깃발을 들고 안들어갈거면 깃발을 내리자
상대편의 깃발을 봤을때 들려있으면(들어가있으면) 기다려야 한다. 만약 안들려있다면(안들어가있다면) 자신의 깃발을 들고 cs에 진입 후 나오면 깃발을 내린다
![](https://images.velog.io/images/langssi/post/831c8065-3bab-4c74-8e1a-bf4e1a4512ac/image.png)
### Mutual Exclusion 위배
![](https://images.velog.io/images/langssi/post/2257dfe4-2c7a-41c5-a86f-35d77f2d06ba/image.png)
cs에 들어가기 직전 preemption이 발생하면 p1이 p0의 flag가 내려가있는 것으로 알고 있기 때문에 cs에 진입하고 p0이 cpu를 다시 할당받고 난 뒤 cs에 진입하면 두 프로세스가 cs에 있게 됨

### v3
![](https://images.velog.io/images/langssi/post/bb77f4d6-9b1f-4b50-afdb-62b0cc018c2e/image.png)
그럼 flag를 먼저 들고 시작해보자

### Progress, Bounded Waiting 위배
![](https://images.velog.io/images/langssi/post/cfbc71f3-1756-499a-87c5-eeba1e4beeaf/image.png)
- flag를 올려두고 preemption이 발생했을때 p1도 flag를 올리고 p0를 확인하면 flag가 올려있는 상태이므로 대기, p0도 다시 cpu를 할당받은 후 p1을 봤을때 flag가 들려있으므로 대기(bw 위배)
- cs가 비어있어도 아무도 진입하지 못함(progress 위배)

