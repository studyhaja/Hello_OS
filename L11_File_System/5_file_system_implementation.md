#### 목차
- Allocation methods
    - File 저장을 위한 디스크 공간 할당 방법
- Free space management
    - 디스크의 빈 공간 관리

# Allocation Methods
- Continuous allocation
- Discontinuous allocation
    - Linked allocation
    - Indexed allocation


## Continuous allocation
![Screen Shot 2021-06-20 at 4 57 15 PM](https://user-images.githubusercontent.com/60768642/122666502-95285b80-d1e8-11eb-9e6b-cfaea6ce0130.png)

## Discontinuous allocation

### Linked Allocation
- 실제로 많이 쓰이는 방법
![Screen Shot 2021-06-20 at 4 58 50 PM](https://user-images.githubusercontent.com/60768642/122666541-ce60cb80-d1e8-11eb-83b4-e537c6010599.png)

![Screen Shot 2021-06-20 at 4 59 57 PM](https://user-images.githubusercontent.com/60768642/122666571-f6502f00-d1e8-11eb-8688-7daa25623a33.png)

### Indexed Allocation
![Screen Shot 2021-06-20 at 5 02 24 PM](https://user-images.githubusercontent.com/60768642/122666605-4d560400-d1e9-11eb-82fc-739ee018b7b1.png)
- Index block 크기에 따라 파일의 최대 크기가 제한 된다는 뜻은?
    - 만약 인덱스 블록이 10개로 제한되있고, 한 블록이 100개의 글자만 가질 수 있다면 최대 수는 1000개로 제한된다.


# Free Space management
- Bit vector
- Linked list
- Grouping
- Counting

#### Bit vector
![Screen Shot 2021-06-20 at 5 05 51 PM](https://user-images.githubusercontent.com/60768642/122666680-cbb2a600-d1e9-11eb-9bb2-a34123004dc6.png)

#### Linked list
- 공간적, 탐색적으로 비효율
![Screen Shot 2021-06-20 at 5 06 12 PM](https://user-images.githubusercontent.com/60768642/122666695-e4bb5700-d1e9-11eb-8a43-c9ec2331c399.png)
#### Grouping
![Screen Shot 2021-06-20 at 5 07 09 PM](https://user-images.githubusercontent.com/60768642/122666711-ff8dcb80-d1e9-11eb-90b0-dd8b6bfcac4a.png)

#### Counting
![Screen Shot 2021-06-20 at 5 08 30 PM](https://user-images.githubusercontent.com/60768642/122666752-2b10b600-d1ea-11eb-912a-7b9de6f07134.png)

