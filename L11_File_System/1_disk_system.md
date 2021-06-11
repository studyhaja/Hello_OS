# Disk System
## Disk pack
- 데이터 영구 저장 장치(비휘발성)

### 구성
![](https://images.velog.io/images/langssi/post/7b1b220b-3dd0-4066-8c61-4ead1a87ce08/image.png)
- Sector
  - 데이터 저장/판독의 물리적 단위
- Track
  - Platter한 면에서 중심으로 같은 거리에 있는 sector들의 집합(원 모양)
- Cylinder
  - 같은 반지름을 갖는 track의 집합
- Platter
  - 양면에 자성 물질(0, 1 표현을 위해서)을 입힌 원형 금속판
  - 데이터의 기록/판독이 가능한 기록 매체
- Surface
  - Platter의 윗면과 아랫면
  
## Disk drive
- disk pack에 데이터를 기록하거나 판독할 수 있도록 구성된 장치
### 구성
![](https://images.velog.io/images/langssi/post/f353876a-9b8b-4554-8c97-ba83ee8ad262/image.png)
- Head
  - 디스크 표면에 데이터를 기록/판독
- Arm
  - Head를 고정/지탱
- Positioner (boom)
  - Arm을 지탱
  - Head를 원하는 track으로 이동
- Spindle
  - Disk pack을 고정(회전축)
  - 분당 회전 수(RPM, Revolutions Per Minute)
    - 높을수록 정보를 빨리 읽을 수 있다.
    
## Disk Address
### Physical disk address
- Sector(물리적 데이터 전송단위)를 지정
  ![](https://images.velog.io/images/langssi/post/7030dbf6-226c-4bd4-a12d-5a47f2fcc171/image.png)
  - 원하는 섹터를 찾아가려면 위의 정보가 모두 필요하다.
- Logical disck address: relative address
  - 사용자는 파일을 저장할때 physical address를 지정하지 않는다. OS의 역할임
    - 하지만, OS가 모든 종류의 하드 디스크의 기계적인 특징들을 다 알 수는 없다.
  - Disk system의 데이터 전체를 block의 나열들로 취급
    - Block에 번호 부여
    - 임의의 block에 접근 가능
    - OS는 블록의 번호로 파일을 저장함
  - Block 번호 -> physical address 모듈 필요(disk driver)
    ![](https://images.velog.io/images/langssi/post/6d51b0b4-6e20-4157-922f-5d98eecc1bb6/image.png)
    
### Disk Address Mapping
![](https://images.velog.io/images/langssi/post/c91edebd-507c-4752-a76b-8f775d6f4c13/image.png)
- Disk driver는 하드웨어 벤더(제조사)들이 가장 잘 알고있으므로 제조사에서 제공 한다.

## Data Access in Disk System
### 1. Seek time
- 디스크 head를 필요한 cylinder로 이동하는 시간
### 2. Roational delay
- 1) 이후에서부터,
- 필요한 sector가 head 위치로 도착하는 시간
### Data transmission time
- 2) 이후에서부터,
- 해당 sector를 읽어서 전송(or 기록)하는 시간
### Disk Access Time
- Seek time + Rotational delay + Data transmission time
