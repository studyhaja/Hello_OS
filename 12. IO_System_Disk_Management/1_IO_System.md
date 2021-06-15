# I/O System(HW)
![](https://images.velog.io/images/langssi/post/d401d5d2-f1eb-402b-9595-090d8334ba72/image.png)
- 프로세서가 메모리에 데이터를 쓰면 그 데이터를 입출력 장치를 통해서 내보낸다.
- 입출력 장치에서 받은 데이터를 메모리에 올린 후 프로세서가 사용한다.

# I/O Mechanisms
## Processor controlled memory access
- CPU가 제어하는 메모리 접근 방법
  - Polling(Programmed I/O)
  - Interrupt
### Polling
- Processor가 주기적으로 I/O 장치의 상태 확인
  ![](https://images.velog.io/images/langssi/post/cad7ba03-e39e-4527-b618-7a9ed87d932d/image.png)
  - 모든 I/O 장치를 순환하면서 확인
  - 전송 준비 및 전송 상태
- 장점
  - Simple
  - I/O 장치가 빠르고, 데이터 전송이 잦은 경우 효율적
- 단점
  - Processor의 부담이 큼(계속 뭔가 할 일이 있는 것)
    - Polling overhead(I/O device가 느린 경우)
### Interrupt
- I/O 장치가 작업을 완료한 후, 자신의 상태를 Processor에게 전달
  ![](https://images.velog.io/images/langssi/post/a26ca1ac-ee8e-420d-9e69-2a9736fd4c51/image.png)
  - Interrupt 발생 시, Processor는 데이터 전송 수행
- 장점
  - Pooling 대비 low overhead
  - 불규칙적인 요청 처리에 적합
- 단점
  - Interrupt handling overhaad
    - Interrupt가 자주 발생하면 오버헤드가 크다.
  
## Direct Memeory Access(DMA)

### Processor controlled memory access 방법
- Processor가 모든 데이터 전송을 처리해야 함
  - High overhead for the proccessor
### Direct Memory Access
- I/O 장치와 Memory 사이의 데이터 전송을 Processor 개입 없이 수행
  ![](https://images.velog.io/images/langssi/post/2072ea5c-bfc6-43a4-953c-35b8703704b8/image.png)
### Processor는 데이터 전송의 시작/종료만 관여
![](https://images.velog.io/images/langssi/post/99bce4f0-d092-410f-a20f-b39d148cbbdf/image.png)

# I/O services of OS
## OS supports for better I/O performance
![](https://images.velog.io/images/langssi/post/5a918702-c768-4ef6-a076-990343747ea4/image.png)
- 커널 입출력 서브 시스템: I/O service 제공

### I/O Scheduling
- 입출력 요청에 대한 처리 순서 결정
  - 시스템의 전반적 성능 향상
  - Process의 요구에 대한 공평한 처리
- E.g., Disk I/O scheduling
### Error handling
- 입출력 중 발생하는 오류 처리
- E.g., disk access fail, network communication error 등
### I/O device information managements
- 입출력 장치 정보 관리

### Buffering
- I/O 장치와 Program 사이에 전송되는 데이터를 Buffer에 임시 저장
  ![](https://images.velog.io/images/langssi/post/d426d465-3168-40ba-97bc-45ffa892d68d/image.png)
  - 입출력 장치와 저장 장치의 속도 차이때문에 버려질 수 있는 데이터를 임시로 저장한다.
- 전송 속도(or 처리 단위) 차이 문제 해결
### Caching
- 자주 사용하는 데이터를 미리 복사해 둠
- Cache Hit시 I/O를 생략할 수 있음
- 참고) 버퍼링은 모아놓았다가 쓰게 하는 것이고, 캐싱은 앞으로 쓰일 데이터를 예측해서 미리 올려놓는 것
### Spooling
- 한 I/O 장치에 여러 Program이 요청을 보낼 시, 출력이 섞이지 않도록 하는 기법(Ex. 여러 파일을 동시에 프린트를 요청했을때)
  ![](https://images.velog.io/images/langssi/post/1f86db09-0fe7-4caa-b26e-83f6b68c5415/image.png)
  - 각 Program에 대응하는 disk file에 기록(spooling)
  - Spooling이 완료 되면, spool을 한번에 하나씩 I/O 장치로 전송
