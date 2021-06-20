## RAID Architecture
- Redundant Array of inexpensive Disks(RAID)
- 여러 개의 물리 disk를 하나의 논리 disk로 사용
  - 비싸지 않은 여러개의 디스크를 모아서 하나의 성능 좋은 디스크처럼 쓰겠다.
  - OS support, RAID controller
- Disk system의 성능 향상을 위해 사용
  - Performance(access speed)
  - Reliability(데이터를 얼마나 안전하게 보관할 수 있는가)
 
## RAID 0
### Disk striping
- 논리적인 한 block을 일정한 크기로 나누어 각 disk에 나누어 저장
### 모든 disk에 입출력 부하 균등 분배
![](https://images.velog.io/images/langssi/post/46736c51-b9e7-4672-bc7a-53bd3993d060/image.png)
- Parallel access
  - 이상적으로는 4개의 디스크를 쓴다면 4배가 빠를 것임
- Performance 향상(I/O 성능 ↑)
### 한 Disk에서 장애시, 데이터 손실 발생
- Low reliability

## RAID 1
- 데이터를 안전하게 보관하는데 초점
![](https://images.velog.io/images/langssi/post/508b2eee-9634-4b1c-ad9d-f8afb8d9858b/image.png)
### Disk mirroring
- 동일한 데이터를 mirroring disk에 중복 저장
### 최소 2개의 disk로 구성
- 입출력은 둘 중 어느 disk에서도 가능
### 한 disk에 장애가 생겨도 데이터 손실 x
- High reliability
### 가용 disk 용량 = (전체 disk 용량/2)

## RAID 3
### RAID 0 + parity disk
![](https://images.velog.io/images/langssi/post/4c687f86-8879-4b33-8c65-4494080c2f95/image.png)
*참고: parity 정보가 있다면 error detection과 데이터를 복구를 할 수 있음
- Byte 단위 분할 저장
- 모든 disk에 입출력 부하 균등 분배
  - Parallel access, performance 향사
### 한 disk에 장애 발생 시, parity 정보를 이용하여 복구
### Write시 parity 계산 필요
- Overhead
- Write가 몰릴 시, 병목현상 발생 가능(패러티 disk는 하나이므로)

## RAID 4
![](https://images.velog.io/images/langssi/post/dcd9ee89-0480-483a-babb-a0ff65702390/image.png)
### RAID 3과 유사, 단 Block 단위로 분산 저장
- 독립된 access 방법
- Disk간 균등 분배가 안 될 수도 있음
- 한 disk에 장애 발생 시, parity 정보를 이용하여 복구
- Write시 parity 계산 필요
  - Overhead/Write가 몰릴 시 병목현상 발생 가능
### 병목 현상으로 성능 저하 가능
- 한 disk에 입출력이 몰릴 때

## RAID 5
![](https://images.velog.io/images/langssi/post/f25e20ea-cd87-44a1-83d3-85b1ce7ea3c1/image.png)
- RAID 4와 유사
  - 독립된 access 방법
- Parity 정보를 각 disk들에 분산 저장(parity disk에 문제가 생기면 에러를 고칠 수 없으므로)
  - ex. A0, B0, C0, D0에 대한 정보를 블록 E의 패러티 0에 저장, A1, B1, C1, E1에 대한 정보를 블록 D의 패러티 1에 저장...
  - 블록 A가 고장나면 다른 블록의 패러티에서 A0, A1, A2, A3 복구 가능
  - Parity disk의 병목 현상 문제 해소
- 현재 가장 널리 사용되는 RAID level 중 하나
  - High performance and reliability
  
![](https://images.velog.io/images/langssi/post/f5925983-dd9e-4d1f-a366-ef9ae29ccacb/image.png)
  
