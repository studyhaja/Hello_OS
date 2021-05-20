# Backgrounds
## 메모리(기억장치)의 종류
![](https://images.velog.io/images/langssi/post/b8a611f7-8761-4226-af2d-1924e0901323/image.png)
- I/O bottleneck 때문에 계층 구조가 발생하게 되었음
- 레지스터와 캐시는 CPU상에 존재하고 HW(CPU)가 관리함
- 메인 메모리와 보조기억장치는 SW(OS)가 관리함 -> 앞으로 공부할 기억장치

## 메모리(기억장치) 계층구조
![](https://images.velog.io/images/langssi/post/33bc06f3-5e53-4250-bc01-6d799e774712/image.png)
### Block
- 보조기억장치와 주기억장치 사이의 데이터 전송 단위
- Size: 1~4KB
- 1bit를 읽더라도 블록 단위로 읽어옴
### Word
- 주기억장치와 레지스터 사이의 데이터 전송 단위
- Size: 16~64bits
- word의 크기가 의미하는 것
  - 32bit, 64bit 컴퓨터? -> word 단위 (완벽한 정답은 아니지만)
  - 이 크기만큼으로 데이터를 한번에 읽어온다.
  
## Address Binding
![](https://images.velog.io/images/langssi/post/cb52b8e8-a9db-4bcf-bb15-4aa2ad1384bd/image.png)
- 프로그램의 논리 주소(ex. `int a;`)를 실제 메모리의 물리 주소로 매핑하는 작업
### Binding 시점에 따른 구분
- Compile time binding
- Load time binding
- Runtime binding
### User Program Processing Steps
![](https://images.velog.io/images/langssi/post/d38ffb21-c788-4f69-8325-8adb77d223d4/image.png)
- 소스코드에서 실제로 메모리에 올라가서 실행되기까지의 과정
- compile: object moudule로 변환
- linker: object module에서 실행가능한 load module로 만드는 작업을 해줌
- load module: 실행파일 
- 실행파일 클릭 -> 메모리에 올라감(로딩)
- 프로세스가 메모리에 올라가면 실행됨 
### Compile time binding
- 프로세스가 메모리에 적재될 위치를 컴파일러가 알 수 있는 경우(컴파일러가 주소를 정해줌)
  - 초창기 컴퓨터들
  - 컴파일러가 메모리를 완벽히 이해하고 있어야한다는 한계점
  - 위치가 변하지 않음(`int a; int b;`라면 항상 같은 위치에 올라가야함)
- 프로그램 전체가 메모리에 올라가야 함
### Load time binding
- 메모리 적재 위치를 컴파일 시점에서 모르면, 대체 가능한 상대 주소를 생성
  - ex. u라는 시점에 시작되었다면 u+100, u-100과 같이 주소를 상대적으로 저장 
- 적재 시점(load time)에 시작 주소를 반영하여 사용자 코드 상의 주소를 재설정
- 프로그램의 전체가 메모리에 올라가야 함
![](https://images.velog.io/images/langssi/post/5133a1df-eadd-4f6d-b959-8f2837199fc3/image.png)
- 시작 주소를 0으로 저장해두었는데 실제로는 400이므로 모두 +400을 해준다 -> 실제 올라간 메모리와 동일해짐(상대주소 -> 절대주소 변환)
### Run-time binding
![](https://images.velog.io/images/langssi/post/198801b1-7226-412e-85ac-cf8053239c5d/image.png)
- Adress binding을 수행시간까지 연기
  - 프로세스가 수행 도중 다른 메모리 위치로 이동할 수 있음
  - ready->running->block 싸이클에서 running이 될때마다 메모리를 새로 설정함
- HW의 도움이 필요
  - MMU: Memory Management Unit
- 대부분의 OS가 사용
## Dynamic Loading
- 앞의 address binding과 다르게 프로그램 전체를 메모리에 올리지 않는 것
- 모든 루틴을 교체 가능한 형태로 디스크에 저장
  - func A, func B, func C를 각각 따로 저장
  - 실제로 함수를 호출했을때 그 함수만 메모리에 올림
- 실제 호출 전까지는 루틴을 적재하지 않음
  - 메인 프로그램만 메모리에 적재하여 수행
  - 루틴의 호출 시점에 address binding 수행
### 장점
- 메모리 공간의 효율적 사용
## Swapping
![](https://images.velog.io/images/langssi/post/a6e3732f-d929-49d4-93c8-ab43ce6e9e3d/image.png)
- swap-out: 프로세서 할당이 끝나고 수행 완료된 프로세스를 swap-device로 보냄
- swap-in: 새롭게 시작하는 프로세스를 메모리에 적재
