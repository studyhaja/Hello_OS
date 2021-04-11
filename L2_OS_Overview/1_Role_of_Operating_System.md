## 운영체제
컴퓨터 하드웨어를 효율적으로 관리하여 사용자/응용프로그램에게 서비스를 제공한다.

## 운영체제의 역할
### User Interface(편리성)
사용자가 시스템을 편리하게 사용할 수 있도록 편리성 제공
- CUI(Character User Interface)
    - 문자기반인 과거에 주로 사용되던 유저 인터페이스
- GUI(Graphical User Interface)
    - 현재 사용되는 그림 형태 기반의 유저 인터페이스
- EUCI(End-User Comfortable Interface)
	- 특별한 목적을 위해서 만들어진 기기의 경우 목적만을 위해 사용자가 편하게 사용할 수 있도록 특화된 인터페이스
    - ex. mp3 player (mp3 사용만을 위한 인터페이스)
    
### Resource Management(효율성)
주어진 자원을 제대로 활용하여 효율성을 높임
- HW Resource(processor, memory, I/O devices, Ect.)
- SW Resource(file, application, message, signal, Etc.)

### Process and Thread Management
프로세스를 관리하는 역할

*Process: 프로그램을 실행하는 주체

### System Management(시스템 보호)
사용자가 불법적인 형태로 시스템을 사용하려고 할때 그로부터 보호함

## 컴퓨터 시스템의 구성
![image](https://user-images.githubusercontent.com/45524783/114297543-1d54fb00-9aec-11eb-8a97-7113b9b3ffb6.png)
### Kernel
운영체제의 핵심을 모아놓은 것(뒤에서 자세히)
### System Call Interface
- 사용자가 직접 커널을 엑세스하거나 조작하면 OS가 하드웨어를 제어하는데 문제를 야기할 수 있으므로 필요한 기능이 있을때 커널에 요청을 하는 통로
- 즉, 커널이 제공하는 기능들 중 사용자가 사용할 수 있는 기능들을 모아놓은 것들
### 커널이 하는 일들
![image](https://user-images.githubusercontent.com/45524783/114297565-35c51580-9aec-11eb-9a8f-d68965fb2609.png)

## 운영체제의 구분
### 동시 사용자수
- Single-user System
	- 한 명의 사용자만 시스템 사용 가능
      - 한 명의 사용자가 모든 시스템 자원 독점
      - 자원 관리 및 시스템 보호 방식이 간단
    - 개인용 장비(PC, mobile) 등에 사용
      - Windows 7/10, Android, MS-DOS 등
- Multi-user System
    - **동시에** 여러 사용자들이 시스템 사용 
      - 각종 시스템 자원(파일 등)들에 대한 소유 권한 관리가 필요
      - OS 기능 및 구조가 복잡
    - 서버, 클러스터 장비 등에 사용
	  - Unix, Linux, Windows server등
    - 동시에 여러 프로세스가 실행될 수 있음
### 동시 실행 프로세스 수
- 단일 작업(Single-tasking System)
  - 시스템 내에 하나의 작업(프로세스)만 존재
    - 하나의 프로그램 실행을 마친 뒤에 다른 프로그램을 실행
  - 운영체제의 구조가 간단
  - ex. MS-DOS
- 다중 작업(Multi-tasking System)
  - 동시에 여러 작업(프로세스)의 수행 가능
    - 작업들 사이의 동시 수행, 동기화 등을 관리해야 함
  - 운영체제의 기능 및 구조가 복잡
  - ex. Unix/Linux, Windows 등

### 작업 수행 방식(사용자가 느끼는 사용 환경)
- Batch Processing System
- Time-sharing System
- Distributed Processing System
- Real-time System
