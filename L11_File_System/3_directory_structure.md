Directory: 파일을 분류해서 사용하기 위해서 필요

## Directory Structure
### Logical directory structure
- Flat(single-level) directory structure
- 2-level directory structure
- Hierarchical (tree-structure) directory structure
- Acyclie graph directory structure
- General graph directory structure

## Flat Directory Structure
![](https://images.velog.io/images/langssi/post/5b9bc172-5449-4988-9628-5af0674336cd/image.png)
### FS(File System)내에 하나의 directory만 존재
- Single-level directory structure
- ex. 초창기 mp3
### Issues
- File naming
  - 이름이 충돌하는 경우가 발생하므로 이름을 짓기 어려움
- File protection
  - 이름이 중복되는 경우 덮어씌워지는 문제가 발생할 수 있음
- File management
  - 파일의 보관이나 분류가 어려움
* 다중 사용자 환경에서 문제가 더욱 커짐

## 2-Level Directory Structure
![](https://images.velog.io/images/langssi/post/c1b77f44-8c4d-403d-95cb-2cd159dfd6b8/image.png)
- 사용자마다 하나의 directory 배정
### 구조
- MFD(Master File Directory)
- UFD(User File Directory)
### Problems
- Sub-directory 생성 불가능
  - File naming issue
- 사용자간 파일 공유 불가
  - 공유하려면 파일 전체에 대한 액세스를 허용해야 하는 보안 이슈 발생
  
## Hierarchical Directory Structure
![](https://images.velog.io/images/langssi/post/a953d74d-9ab4-4435-a730-3d95176dbeca/image.png)
- Tree 형태의 계층적 directory 사용 가능
- 사용자가 하부 directory 생성/관리 가능
  - System call이 제공되어야 함
  - Terminologies
    - Home directory(나에게 할당된 디렉토리중 최상단 디렉토리), Current directory
    - Absolute pathname, Relative pathname
- 대부분의 OS가 사용

## Acyclic Graph Directory Structure
![](https://images.velog.io/images/langssi/post/3a78fa73-de3d-4f55-ab2b-376f73463819/image.png)
*Acycile: 루프가 될 수 없음
- Hierarchical directory structure 확장
- Directory안에 shared directory, shared file를 담을 수 있음
- Link의 개념 사용(윈도우의 바로가기)
  - E.g., Unix system의 symbolic link
  
## General Graph Directory Structure
![](https://images.velog.io/images/langssi/post/72a5e0eb-2787-42ba-9b9a-351c9acba63d/image.png)
- Acycile Graph Directory Structure의 일반화
  - Cycle을 허용
### Problems
  - File 탐색시, Infinite loop를 고려해야함
