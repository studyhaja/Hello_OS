# Mutual Exclusion Solutions
## SW solutions
- Dekker's algorithm
- Dijkstra's algorithm
## HW solution
- TestAndSet(TAS) instruction
## OS supported SW solution
- Spinlock
- Semaphore
- Eventcount/sequencer
## Laqnguage-Level solution
- Monitor

## 주제: Semaphore
- 1965년 Dijkstra가 제안
- Busy waiting 문제 해결
- Semaphore는 음이 아닌 정수형 변수이다(S)
  - S에는 초기화 연산인 P()와 V()로만 접근이 가능하다
    - P: Probern(검사)
    - V: Verhogen(증가)
- ***임의의 S 변수 하나에 ready queue하나가 할당된다.***
![스크린샷 2021-04-24 오전 10 36 44](https://user-images.githubusercontent.com/60768642/115943114-10230d80-a4e9-11eb-856d-a03198a1666d.png)
### Binary semaphore vs Counting semaphore
#### Binary semaphore
- S가 0 또는 1
- 상호배재, 프로세스 동기화에 사용됨
#### Counting semaphore
- S가 0이상 정수값을 가짐
- Producer-Consumer 문제 등을 해결하기 위해 사용됨.

### 초기화연산, P(), V()연산
#### 초기화 연산
- S 변수에 초기값을 부여하는 연산
#### P(), V()연산
![스크린샷 2021-04-24 오전 10 47 41](https://user-images.githubusercontent.com/60768642/115943378-93912e80-a4ea-11eb-90ca-ce783f7b0735.png)
- 스핀락은 P() else일 경우 계속 while 도는 반면, semaphore는 대기실(큐)에서 기다리므로 busy wating해결. 이게 spinlock과의 가장 큰 차이.
#### 모두 indivisible 연산
- 나눌 수 없는, 한 번에 실행되는
- by OS support
- 전체가 하나의 instruction cyle로 수행됨.

### Semaphore로 해결 가능한 동기화 문제들
- 상호배제 문제(Mutual exclusion)
- 프로세스 동기화 문제(process sychronization problem)
- 생산자-소비자 문제(producer-consumer problem)
- reader-writer 문제
- Dining philosopher problem
- 기타

#### Mutual exclusion
![스크린샷 2021-04-24 오전 10 51 14](https://user-images.githubusercontent.com/60768642/115943471-1c0fcf00-a4eb-11eb-8573-8dbc315fd3fd.png)

#### Process synchronization
- Process들의 실행 순서 맞추기
  - 프로세스들은 병행적이며, 비동기적으로 수행
![스크린샷 2021-04-24 오전 10 54 02](https://user-images.githubusercontent.com/60768642/115943541-7315a400-a4eb-11eb-92d3-2180fd182f59.png)

- sync라는 세마포어 변수를 0으로 초기화(물건이 없는 상태)
- 물건은 Pj가 들고 있었다고 가정.
- Pi가 먼저 도착해서 기다리고 있었을 경우, 물건이 없으므로 Li 에서 물건 기다림(Queue)
- Pj가 Lj 지나가면서 Pi 꺠워주고 감
- 만약 Pi가 더 늦게 도착했다면, Pj는 지나가면서 물건만 반납하고(sync=1) 가면 됨. 이 경우엔 깨워주지 않고 지나감(깨울 사람이 없으니까 당연)
![스크린샷 2021-04-24 오전 10 58 02](https://user-images.githubusercontent.com/60768642/115943625-f46d3680-a4eb-11eb-93b0-6b07908f5bc2.png)

#### Producer-Consumer problem
- Producer process: 메시지 생성하는 프로세스 그룹
- Consumer process: 메시지 전달받는 프로세스 그룹
- 생산자, 소비가 간의 동기화가 필요함.
- 조건 1: Producer가 buffer에 물건 올려놓는 동안에 Consumer가 들어와서 가져가려 하면 안됨, 혹은 물건을 꺼내가는 동안 놓으며 안됨.
- 조건 2: 이미 buffer에 물건 있다면 Producer가 물건 또 놓으려고 하면 안됨.
![스크린샷 2021-04-24 오전 10 59 59](https://user-images.githubusercontent.com/60768642/115943675-54fc7380-a4ec-11eb-848c-06efe0ddcadf.png)
#### Producer-Consumer single buffer인 경우
![스크린샷 2021-04-24 오전 11 03 21](https://user-images.githubusercontent.com/60768642/115943731-bb819180-a4ec-11eb-9883-20548a79af57.png)
- var consumed: 소비 되었니?(확인)
- var produced: 생산 되었니?(확인)
```
Procuder
1. 메세지 생성
2. 소비 되었니? 확인(버퍼가 비었는지 확인) P연산(검사연산). P(consumed)
3. 비었으면 생성한 메시지 버퍼에 두기
4. 생산량 1 증가시킴. V연산(증가). V(produced). Consumer queue에 자는 애 있으면 꺠워줌.
```
#### Producer-Consumer N-buffer인 경우
![스크린샷 2021-04-24 오전 11 09 04](https://user-images.githubusercontent.com/60768642/115943885-80cc2900-a4ed-11eb-83e4-bf04d9c97e80.png)
![스크린샷 2021-04-24 오후 5 46 27](https://user-images.githubusercontent.com/60768642/115953207-0a4b1d80-a525-11eb-9ef0-5f7bfee3b238.png)
```
var nrfull: 채워진 buffer 수
var nrempty: 비어있는 buffer 수
mutexP: producer간 상호 배제.(한 번에 한 producer만 일할 수 있음.)
mutexC: consumer간 상호 배제(한 번에 한 consumer만 일할 수 있음.)

Producer Pi
1. create a new message M : 메세지 생성
2. P(mutexP); 현재 일하고 있는 producer가 있는지 확인.
3. P(nrempty): 빈 버퍼가 있는지 확인. 있다면 들어가고 없다면 queue에서 대기
4. buffer[in] <- M 해당하는 버퍼에 물건(메세지)을 놓음
5. in <- (in +1) mod N; 다음 버퍼 위치를 갱신시켜줌(circular queue를 쓰기 때문에 다음 위치를 갱신해줘야 함)
6. V(nrfull) 물건 수 하나 늘렸다고 표시해줌
7. V(mutexP) 상호배제 표시 해제하고 나옴.
```


#### Reader-Writer problme
- Reader
  - 데이터 읽기 연산 수행(동시에 여러명이 읽어도 됨)
- Writer
  - 데이터 갱신 연산 수행(동시에 딱 한명만 작업해야 함)
- 데이터 무결성 보장이 필요하다!
  - Reader들은 동시에 데이터 접근 가능
  - Writer들(또는 reader와 writer)이 동시 데이터 접근 시, 상호 배제(동기화) 필요
- 해결법
  - reader / writer 에 대한 우선권 부여
    - reader preference solution
    - writer preference solution
    
![스크린샷 2021-04-24 오후 5 57 34](https://user-images.githubusercontent.com/60768642/115953448-914cc580-a526-11eb-8aa3-e3224d673399.png)
```
Writer Wj는 엄청 간단하다.
- writer mutex 걸고
- write작업 완료 후
- write mutex 해제하고 나온다.
```

```
Reader Ri
1. P(rmutex) : 읽기 mutex를 걸어준다
read행위 자체는 동시에 여러 reader가 할 수 있지만,
reader 수 +1하거나, wmutex 거는 작업은 동시 진행이 불가능하기 때문에 Rmutex를 걸어준다.
2. nreaders >0 이면 wmutex가 이미 걸려있을 테니 if문 바로 빠져나오고,
nreaders = 0 이라면 내가 일빠(?)인 셈이니 wmutex를 걸어준다.
3. reader숫자 +1 
4. V(rmutex) rmutex를 해제한다.
5. read작업 수행!
6. P(rmutex): 다 읽은 후 reader -1 해주고, 내가 마지막 reader라면 wmutex도 해제하고 나온다.
이를 동시에 여러 reader가 하면 안되니 rmutex를 걸어준다.

```

#### Semaphore 정리
- ***No busy waiting***
  - 기다려야 하는 프로세스는 block(asleep) 상태가 됨
- ***Semaphore queue에 대한 wake-up 순서는 비결정적***
  - queue에 있는 애 중 누구를 깨울지 정해진 규칙 없이 랜덤으로 깨움(사실상 queue라기 보다는 대기실인듯)
  - (다음 강의에선 누구를 깨울지에 관한 내용이 나온다고 한다.)


## 주제: Eventcount/Sequencer
- semaphore가 busy waiting의 문제는 해결 했지만, queue에 있는 애들 중 누구를 먼저 꺠울지 정해지지 않았기에 <br>
starvation 문제가 발생할 수 있었다. 이번에는 이 문제를 해결해보자.
![스크린샷 2021-04-25 오후 2 56 19](https://user-images.githubusercontent.com/60768642/115982943-6d968780-a5d9-11eb-87ed-6540832bf750.png)

- eventcount/sequencer: 은행의 번호표와 비슷한 개념
#### Sequencer
- 정수형 변수(초기값: 0)
- 생성시 0으로 초기화, 감소하지 않음
- 발생 사건들의 순서 유지
- ticket() 연산으로만 접근 가능

#### ticket(S)
- 현재까지 ticket() 연산이 호출 된 횟수를 반환
- Indivisible operation

#### eventcount
- 정수형 변수
- 생성시 0으로 초기화, 감소하지 않음
- 특성 사건의 발생 횟수를 기록
- read(E), advance(E), await(E, v) 연산으로만 접근 가능

#### read(E)
- 현재 Eventcount값 반환

#### advance(E)
- E <- E + 1
- E를 기다리고 있는 프로세스를 꺠움(wake-up)

#### await(E, v)
- V는 정수형 변수
- if (E < v)이면 E에 연결된 Qe에 프로세스 전달(push) 및 CPU scheduler 호출
```
- 번호표 띵동 하는 기계가 이벤트 카운트라고 보면 된다.
111이라 써있으면 111명의 손님을 처리했고 111번째 손님 오라는 것처럼 eventcount도 같은 기능을 한다.
- advance: 은행원이 버튼을 눌러서 번호를 1 증가시키는 행위
- await(E,v): E는 현재 번호, v는 내 번호. 내 번호가 E보다 크면 E=v 될 때 까지 대기실에서 대기하고, scheduler에게 나 꺠워달라고 부탁함.
```

###  Eventcount/Sequencer로 Mutual exclusion 해결하기
![스크린샷 2021-04-25 오후 3 26 23](https://user-images.githubusercontent.com/60768642/115983175-9e2af100-a5da-11eb-8a65-f4c1853cfdf1.png)
```
1. v <- ticket(S);   프로세스가 도착해서 번호표를 발급 받는다. 첫 손님이니 v는 0번이다.
2. await(E, v);  E도 0이고 내 번호표(v)도 0번이니 바로 CS로 들어가서 할 일을 한다.
3. 이때 두 번째 프로세스가 도착해서 ticket(S)을 한다. 두 번째 손님이니 v는 1이다.
4. await(E,v)에서 E는 0(현재 진행중인 손님번호)이고 v는 1이므로 대기실에 가서 쉰다.
5. 첫 손님이 볼 일 다 보고 빠져나가면 E가 0에서 1이 되면서 두번쨰 손님이 CS로 들어간다.

티켓을 뽑고 기다리는게 semaphore의 P연산,
advance는 semaphore의 V연산과 같다.

```

### Eventcount/Sequencer로 Producer-Consumer 해결하기
![스크린샷 2021-04-25 오후 3 22 26](https://user-images.githubusercontent.com/60768642/115983081-23fa6c80-a5da-11eb-82ee-0eecee6e6b4f.png)
```
- var Pticket: producer sequencer
- var Cticket: consumer sequencer
- In: 물건을 놓는 event
- Out: 물건을 꺼내는 event
- Buffer: 크기가 N인 버퍼(물건 놓을 공간)
```
```
Producer Pi
t <- ticket(Pticket);
await(In, t);
위 두 연산을 합쳐서 P()연산으로 볼 수 있고,
advance(In); 연산을 V()연산으로 볼 수 있다.

await(Out t-N+1)과 buffer[t mod N] <- M이 critical section이다.

1. Create a new message M   : 메세지를 생산함
2. t <- ticket(Pticket);    : 티켓을 뽑는다.
3. await(In, t);            : 내 번호가 불릴 때까지 기다리고 불리면 들어간다.
4. await(Out, t-N+1)        : 공간이 있는지 확인하는 과정.(요게 좀 어렵고 복잡합니다. 아래 설명을 잘 보세요)
  - 공간이 있다는 건 '공간 >= 1' 이라는 의미이죠.
  - 공간은 기본 N개에, t개만큼 뺴줘야 하고(물건을 놓은 수), 다시 Out만큼 더해줘야 합니다.
  - 즉 N - t + Out >= 1 입니다.
  - await은 Eventcounter가 좌변에 오게 되있고, < 수식으로 표현하므로 이에 맞게 바꿔줍니다..
  * await의 정의: if (E < v)
  - Out >= t - N + 1
  최종결과: Out < t - N + 1
5. buffer[t mod N] <- M     : 버퍼에 물건을 놓는다.

```

```
Counsumer Cj
u <- ticket(Cticket);, await(Out, u); 두개를 합쳐서 P()연산을 볼 수 있고,
advance(Out)을 V()연산으로 볼 수 있다.


1. u <- ticket(Cticket);      : ticket 뽑는다.
2. await(Out, u);             : 내 순서 될 때까지 기다린다.
3. await(In, u + 1);          :  물건이 있을 때까지 기다린다.
  - 물건이 있다는 건 물건 >= 1
  - 물건은 In(물건 놓은 수) - u로 정의할 수 있다.
  - In -u >= 1
  - 이를 await에 맞게 정리하면?
  - In < u + 1
4. m <- buffer[u mod N]       : 물건을 꺼내온다.
```

#### eventcount/ sequencer 정리
- No busy wating
- No starvation
  - FIFO scheduling for Qe
- Semaphore보다 더 low-level control이 가능(무슨 말일까)
  - 순서를 컨트롤 할 수 있다는 말을 위처럼 표현한다고 한다.
  

## Language-Level solution
![스크린샷 2021-04-25 오후 3 46 41](https://user-images.githubusercontent.com/60768642/115983654-79844880-a5dd-11eb-8c98-e09e6fa66c9d.png)
- 여태 했던 방법들은 Low-level mechanism이다.
- 이번에 할 것은 language-level에서 해결하는 방법으로 High-level mechanism으로 분류된다.

#### High-level Mechanism
- ***Monitor***
- Path expressions
- Serializers
- Ctirical region, conditional critical region

- 위 네가지 중 우리는 Monitor만 보기로 한다.
- Language-level constructs. 언어 단에서 상호배제를 지원한다.
- Object-Oriented concept와 유사하다.
- 사용이 쉽다.

### Monitor
- Monitor은 Critical data(공유 데이터), Critical section을 모아놓은 방이라고 생각하면 된다.
- 이 방엔 한 번에 한 명만 들어올 수 있다.
- critical data는 빌리려는 책, critical section은 책을 빌리기 위해 대출 등의 작업을 하는 연산이라고 생각하면 된다.
- Conditional variable(wait(), signal()이 존재한다. 뒤에서 설명함)
![스크린샷 2021-04-25 오후 3 50 40](https://user-images.githubusercontent.com/60768642/115983740-06c79d00-a5de-11eb-870e-0857f1a1be70.png)

#### Monitor의 구조
- Entry Queue(진입 큐)
  - 모니터 내의 procedure(func) 수만큼 존재
- Mutual exclusion(monitor의 특성)
  - 모니터 내에는 항상 하나의 프로세스만 진입 가능(책방에 한 명만 들어올 수 있음)
- Information hiding(정보 은폐)(monitor의 특성)
  - 공유 데이터는 모니터 내의 프로세스만 접근 가능
- Condition queue(조건 큐)
  - 모니터 내의 특정 이벤트를 기다리는 프로세스가 대기(하는 방)
- Signaler queue(신호제공자 큐)
  - 모니터에 항상 하나의 신호제공자 큐가 존재
  - signal() 명령을 실행한 프로세스가 임시 대기
  - (condition queue에 "다음 너 차례니까 나와라" 라고 전화 거는 전화부스 같은 곳)
#### 자원 할당 시나리오
  ![스크린샷 2021-04-25 오후 3 50 40](https://user-images.githubusercontent.com/60768642/115985061-0979c080-a5e5-11eb-91c1-df8e6b854fba.png)
![스크린샷 2021-04-25 오후 4 40 11](https://user-images.githubusercontent.com/60768642/115985062-0bdc1a80-a5e5-11eb-96d7-6d087102fef9.png)
![스크린샷 2021-04-25 오후 4 40 16](https://user-images.githubusercontent.com/60768642/115985065-0d0d4780-a5e5-11eb-8bfe-cf1c16b5565b.png)
![스크린샷 2021-04-25 오후 4 40 21](https://user-images.githubusercontent.com/60768642/115985067-0da5de00-a5e5-11eb-9749-cca97662b288.png)
![스크린샷 2021-04-25 오후 4 40 31](https://user-images.githubusercontent.com/60768642/115985068-0e3e7480-a5e5-11eb-82a8-a12de0249767.png)
![스크린샷 2021-04-25 오후 4 40 41](https://user-images.githubusercontent.com/60768642/115985069-0ed70b00-a5e5-11eb-8d54-88827e207bfc.png)
![스크린샷 2021-04-25 오후 4 40 47](https://user-images.githubusercontent.com/60768642/115985071-0ed70b00-a5e5-11eb-8a5d-464451b59033.png)

#### producer-consumer problem
- entry queue for fillBuf(): Producer 
- entry queue for emptyBuf(): consumer 
- bufHasData: 물건 있니?(conditional queue, consumer가 물건 없을 때 기다리는 queue)
- bufHasSpace: 빈공간 있니?(conditional queue, produce가 공간 없을 때 기다리는 queue)
- in: 물건 어디에 넣을지 위치
- out: 물건 어디서 빼갈지 위치 
- validBufs: 물건수
![스크린샷 2021-04-25 오후 4 42 51](https://user-images.githubusercontent.com/60768642/115985147-73926580-a5e5-11eb-939d-7d8b28ae0c94.png)
![스크린샷 2021-04-25 오후 4 43 57](https://user-images.githubusercontent.com/60768642/115985153-7a20dd00-a5e5-11eb-8ee2-6646848efa3c.png)
```
procedure fillBuf
1. if (validBuf = N) then bufHasSpace.wait();
-> 공간이 있는지 확인하고 없으면 대기. (validBuf는 물건수. 물건수가 N이면 공간이 없다는 뜻)
2. buffer[in] <- data
-> 공간이 생기면 들어가서 물건을 놓는다.
3. validBufs <- validBufs + 1;
-> 물건 수를 하나 증가시켜준다.
4. in <- (in + 1) Mod N;
-> 다음에 물건 놓을 공간을 갱신시켜준다(버퍼가 N개일 때 하는 연산)
5. bufHasData.signal();
-> 버퍼에 데이터가 있다고 알려주는 연산 시행(물건 오길 기다리는 consumer를 깨워줌)
```

#### Reader-Writer Problem
- 이건 숙제라고, 직접 해보라고 하십니다.
![스크린샷 2021-04-25 오후 4 51 52](https://user-images.githubusercontent.com/60768642/115985379-940eef80-a5e6-11eb-9906-c1c0104b890f.png)
![스크린샷 2021-04-25 오후 4 51 56](https://user-images.githubusercontent.com/60768642/115985386-98d3a380-a5e6-11eb-9276-236cc859ff52.png)

#### Dining philosopher problem
- 5명의 철학자
- 철학자들은 생각하는 일과 스파게티 먹는 일만 반복함
- 공유 자원: 스파게티, 포크
- 스파게티를 먹기 위해서는 좌우 포크 2개를 모두 들어야 함.
- 철학자: Process
- 포크: shared data
![스크린샷 2021-04-25 오후 4 54 16](https://user-images.githubusercontent.com/60768642/115985457-e4864d00-a5e6-11eb-8561-6161eb3d7d4f.png)
- 각 철학자는 각자의 ready queue가 있음.
![스크린샷 2021-04-25 오후 4 55 12](https://user-images.githubusercontent.com/60768642/115985570-68403980-a5e7-11eb-9d86-d1a97f0b7cad.png)
![스크린샷 2021-04-25 오후 4 55 30](https://user-images.githubusercontent.com/60768642/115985574-6aa29380-a5e7-11eb-944e-e430fee65c4f.png)
![스크린샷 2021-04-25 오후 4 56 20](https://user-images.githubusercontent.com/60768642/115985581-6d04ed80-a5e7-11eb-900d-d4d4531504e1.png)
![스크린샷 2021-04-25 오후 4 56 36](https://user-images.githubusercontent.com/60768642/115985582-6d9d8400-a5e7-11eb-9704-abf9aca45536.png)

-심심하면 위 문제를 semaphore로 풀어보세요^^ by 교수님

#### Monitor 정리
- 장점
  - 사용이 쉽다.
  - Deadlock 등 error 발생 가능성이 낮음
- 단점
  - 지언하는 언어에서만 사용 가능
  - 컴파일러가 OS를 이해하고 있어야 함
    - Critical section 접근을 위한 코드 생성
