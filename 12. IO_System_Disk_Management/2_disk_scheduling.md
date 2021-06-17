## Disk Scheduling
- Disk access 요청들의 처리 순서를 결정
- Disk system의 성능을 향상
### 평가 기준
- Throughput
  - 단위 시간당 처리량
- Mean response time
  - 평균 응답 시간
- Predictability
  - 응답 시간의 예측성
  - 요청이 무기한 연기(staravtion)되지 않도록 방지

### Data Access Time
1. Seek time
- 디스크 head를 필요한 cylinder로 이동하는 시간
2. Roational delay
- 1 이후에서 부터
- 필요한 sector가 head 위치로 도착하는 시간
3. Data transmission time
- 2 이후에서 부터
- 해당 sector를 읽어서 전송(or 기록)하는 시간

## Scheduling Methods
### Optimizing seek time
- FCFS(First Come Fisrt Service)
- SSTF(Shortest Seek Time First)
- Scan
- C-Scan(Circular Scan)
- Look
### Optimiaing rotational delay
- Sector queueing(SLTF, Shortest Latency Time First)
### SPTF(Shortest Positioning Time First)

# Seek Time Optimizing
## First Come Fisrt Service(FCFS)
- 요청이 도착한 순서에 따라 처리
### 장점
- Simple
  - Low scheduling overhead
- 공평한 처리 기법(무한 대기 방지)

### 단점
- 최적 성능 달성에 대한 고려가 없음

### Disk access 부하가 적은 경우에 적합
### Example
- 총 256개의 cylinder으로 구성
- Head의 시작 위치: 100번 cylinder
- Access request queue
![](https://images.velog.io/images/langssi/post/6bc59d0c-54b5-4613-b0c0-e931fd5aca66/image.png)

## Shortest Seek Time Fisrt(SSTF)
- 현재 head 위치에서 가장 가까운 요청 먼저 처리
### 장점
- 이동거리 ↓, Throughput ↑
- 평균 응답 시간 ↓

### 단점
- 가까운 요청부터 먼저 처리하므로 Predictability ↓
- Starvation 현상 발생 가능
### 처리량이 많고 응답시간이 크게 상관 없는 일괄처리 시스템에 적합
![](https://images.velog.io/images/langssi/post/43ea53e1-5f49-471f-a34c-f5e8333ba379/image.png)

## Scan Scheduling
- 현재 head의 진행 방향에서 head와 가장 가까운 요청 먼저 처리
- (진행방향 기준) 마지막 cylinder 도착 후, 반대 방향으로 진행

### 장점
- SSTF의 starvation 문제 해결(진행 방향 쪽에 있다면 언젠간 도착한다는 것을 예상한다)
- Throughput 및 평균 응답시간 우수
### 단점
- 진행 방향 반대쪽 끝의 요청들의 응답시간 ↑
![](https://images.velog.io/images/langssi/post/4dcd08dc-5f2f-4bf1-97c0-e3c9aad82346/image.png)

## C-Scan Scheduling
- SCAN과 유사
- Head가 미리 정해진 방향으로만 이동
  - 시작점에서 다시 시작하게 되면 이미 거쳐갔던 곳들이 두 번의 기회를 얻게되므로 맨 마지막 cynlinder 입장에서는 불공평하다.
  - 마지막 cylinder 도착 후, 시작 cylinder 이동 후 재시작
### 장점
- Scan 대비 균등한 기회 제공
### 단점
- 불필요한 이동 ↑
![](https://images.velog.io/images/langssi/post/8173453a-7873-48bb-85fd-1f1ada98c85a/image.png)

## Look Scheduling
- Elevator algorithm
- Scan(C-Scan)에서 현재 진행 방향에 요청이 없으면 방향 전환
  - 마지막 cylinder까지 이동하지 않음
  - Scan(C-Scan)의 실제 구현 방법
### 장점
- Scan의 불필요한 head 이동 제거
![](https://images.velog.io/images/langssi/post/ddfe8ad2-1892-4c2c-86d7-7839fb8d8f72/image.png)

# Optimizing Rotational Delay
- disk가 돌아가는 시간을 줄임
## Shortest Latency Time First(SLTF)
- Fixed head disk 시스템에 사용
  - 각 track마다 head를 가진 disk
    - e.g., drum disk
  - Head의 이동이 없음
- Sector queuing algorithm
  - 각 sector별 queue 유지
  - Head 아래 도착한 sctor의 queue에 있는 요청을 먼저 처리 함
![](https://images.velog.io/images/langssi/post/e405be85-8775-4f74-b076-550b3e7e2956/image.png)

- Moving head disk의 경우
- 같은 cylinder 또는 track에 여러 개의 요청 처리를 위해 사용 가능
  - Head가 특정 cylinder에 도착하면 고정 후 
  - queue에 넣어둔 해당 cylinder의 요청을 모두 처리
  
## Shortest Positioning Time First(SPTF)
- Positioning time = Seek time + rotational delay (원하는 위치에 head를 갖다 놓는데까지 걸리는 시간)
- Positioning time이 가장 작은 요청 먼저 처리
### 장점
- Throughput ↑, 평균 응답 시간 ↓
### 단점
- 가장 안쪽(작은 원)과 바깥쪽(바깥 원) cylinder의 요청에 대해 starvation 현생 발생 가능
### Echenbach scheduling
- Positioning time 최적화 시도
![](https://images.velog.io/images/langssi/post/ff8c1df1-b702-4602-9053-a34c66471ee6/image.png)
- Disk가 1회전 하는 동안 최대한의 요청을 처리할 수 있도록 요청을 정렬
  - 한 cylinder내 track, sctor들에 대한 다수의 요청이 있는 경우, 다음 회전에 처리 됨
- 단점
  - 요청이 하나의 cylinder에 몰려있는 경우 하나만 처리하고 이동해야므로 성능이 떨어질 수 있다.
