# 4. 운영체제의 기능
## 요약
- 프로세스 관리
- 프로세서 관리
- 메모리 관리
- 파일 관리
- 입출력 관리
- 보조 기억 장치 및 기타 주변장치 관리


### Process Management
#### 프로세스란?
- 커널에 등록된 실행 단위(실행 중인 프로그램)
- 사용자 요청/프로그램의 수행 주체(entity)
#### OS의 프로세스 관리 기능들
- 생성/삭제, 상태관리
- 자원 할당
- 프로세스 간 통신 및 동기화(synchronization)
- 교착상태(deadlock) 해결
#### 프로세스 정보 관리
- PCB (Process Control Bloc)

### processor Management
#### 프로세서란?
- 중앙 처리 장치(CPU)
  - 프로그램을 실행하는 핵심 자원
- 큰 그림에서는 프로세서=cpu라고 이해해도 크게 문제 되진 않음
#### 프로세스 스케줄링
- 시스템 내의 프로세스 처리 순서 결정
#### 프로세서 할당 관리
- 프로세스들에 대한 프로세서 할당
  - 한 번에 하나의 프로세스만 사용 가능
  
### Memory Management
#### 주기억장치
- 작업을 위한 프로그램 및 데이터를 올려 놓는 공간
#### Multi-user, Multi-tasking 시스템
- 프로세스에 대한 메모리 할당 및 회수
- 메모리 여유 공간 관리
- 각 프로세스의 할당 메모리 영역 접근 보호
#### 메모리 할당 방법(scheme)
(뒷 강의에서 다룰 예정)
- 전체 적재
  - 장점: 구현이 간단 
  - 단점: 제한적 공간
- 일부 적재(virtual memory concept)
  - 프로그램 및 데이터의 일부만 적재
  - 장점: 메모리의 효율적 활용
  - 단점: 보조기억 장치 접근 필요
  
 ### File Management
 -파일: 논리적 데이터 저장 단위
 - 사용자 및 시스템의 파일 관리
 - 디렉토리 구조 지원
 - 파일 관리 기능
   - 파일 및 디렉토리 생성/삭제
   - 파일 접근 및 조작
   - 파일을 물리적 저장 공간으로 사상(mapping)
   - 백업 등

### I/O Management
- 입출력(I/O) 과정
  - OS를 만드시 거쳐야 함
  ![](https://images.velog.io/images/kpl5672/post/566839da-4711-4064-bff3-28596ec68106/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.50.14.png)
  
### Others
- Disk 관리
- networking 관리
- Security and Protection System관리
- Command interpreter system관리
- System call interface관리
  - 응용 프로개름과 os 사이의 인터페이스
  - os가 응용프로그램에 제공하는 서비스
