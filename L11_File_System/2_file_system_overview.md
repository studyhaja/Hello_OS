## File System
- 사용자들이 사용하는 파일들을 관리하는 운영체제의 한 부분
## File system의 구성
### Files
- 연관된 정보의 집합
### Directory structure
- 시스템 내 파일들의 정보를 구성 및 제공
### Partitions
- Directory들의 집합을 논리적/물리적으로 구분
- ex. C드라이브, D드라이브...

## File Concept
### 보조 기억 장치에 저장된 연관된 정보들의 집합
- 보조 기억 장치 할당의 최소 단위
- Sequence of bytes(물리적 정의)
### 내용에 따른 분류
- Program file
  - Source program, object program, executable files
- Data file
### 형태에 따른 분류
- Text(ascii) file
- Binary file

### File attributes(속성)
![](https://images.velog.io/images/langssi/post/aa9d0da2-13cc-4002-af74-8d3b43a63240/image.png)
- Name
- Identifier
- Type
- Location
- Size
- Protection
  - access control information
- User identification(owner)
- Time, date
  - creation, late reference, last modification
  
### File operations
- Create
- Write
- Read
- Reposition(파일을 옮김)
- Delete
- Etc.
**=> OS는 file operation들에 대한 system call을 제공해야 함**

## File Access Methods
### Sequential access(순차 접근)
- File을 record(or byese) 단위로 순서대로 접근(위에서부터 순서대로 읽는다)
  - E.g., fgetc()
### Directed access(직접 접근)
- 원하는 Block을 직접 접근(필요한 부분을 바로 찾아감. 순차적x)
  - E.g., lseek(), seek()
### Indexed access
- Index를 참조하여 원하는 block을 찾을 후 데이터에 접근

## File System Organization
### Partitions(minidisks, volumns)
![](https://images.velog.io/images/langssi/post/298c1109-123b-43f7-9e39-dd7ad9770766/image.png)
![](https://images.velog.io/images/langssi/post/c9866e79-7d7b-45e4-b9ab-d67ae632c344/image.png)
- 논리적으로 나누어놓은 디스크
- Virtual disk
### Directory
- File들을 분류, 보관하기 위한 개념
- Operation on directory
  - Search for a file
  - Create a file
  - Delete a file
  - List a directory
  - Rename a file
  - Traverse file system
  => 다양한 오퍼레이션들은 OS가 **시스템 콜**을 통해서 제공해주어야 한다.
  
### Mounting
![](https://images.velog.io/images/langssi/post/62e0d501-2eb1-48a9-b3aa-44bf19932cb6/image.png)
- 현재 FS에 다른 FS를 붙이는 것
