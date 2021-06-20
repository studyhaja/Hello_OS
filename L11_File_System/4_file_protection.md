- File에 대한 부적절한 접근 방지
    - 다중 사용자 시스템에서 더욱 필요
- 접근 제어가 필요한 연산들
    - Read(R)
    - Write(W)
    - Execute(X)
    - Append(A)

## File Protection Mechanism
- 파일 보호 기법은 system size 및 응용 분야에 따라 다를 수 있음

### Password 기법
- 각 file들에 pw부여
- 비현실적
    - 사용자들이 파일 각각에 대한 pw를 기억해야 함.
    - 접근 권한 별로 서로 다른 pw를 부여해야 함.

### Access Matrix 기법
- 범위(domain, 사용자)와 개체(object, 파일) 사이의 접근 권한을 명시
#### Terminologies
- Object
    - 접근 대상(file, device 등 HW/SW objects)
- Domain(protection domain)
    - 접근 권한의 집합
    - 같은 권한을 가지는 그룹(사용자, 프로세스)
- Access right
    -\ <object-name, rights-set\>

![Screen Shot 2021-06-20 at 4 41 12 PM](https://user-images.githubusercontent.com/60768642/122666123-6c9f6200-d1e6-11eb-9928-d23e7b3a9893.png)

#### Implementation
- Global table
- Access list
- Capability list
- Lock-Key mechanism

#### Global table
![Screen Shot 2021-06-20 at 4 43 08 PM](https://user-images.githubusercontent.com/60768642/122666164-a708ff00-d1e6-11eb-9a24-8bd3a4f4b9f7.png)

#### Access list
![Screen Shot 2021-06-20 at 4 46 00 PM](https://user-images.githubusercontent.com/60768642/122666214-02d38800-d1e7-11eb-87b1-9bc00150e8ba.png)

- 파티 입장 시 초대명부에 내 이름이 있는지 확인하고 들여보내줌.
- 단점은 잠깐 나왔다가 다시 들어갈때도 매 번 명부 대조해서 이름 확인해야 함.(overhead)
- 부페나 놀이공원처럼 손목에 입장 도장 찍어주는 게 capability list임
#### Capability list
- 신분증 같은 시스템
![Screen Shot 2021-06-20 at 4 48 34 PM](https://user-images.githubusercontent.com/60768642/122666293-5fcf3e00-d1e7-11eb-8e6f-e7efcb4bee4a.png)

#### Lock-Key mechanism
- 이런 방법이 있다 정도만 알고 넘어가면 됨.
![Screen Shot 2021-06-20 at 4 50 07 PM](https://user-images.githubusercontent.com/60768642/122666339-986f1780-d1e7-11eb-81a3-edf6b936f874.png)


##### 비교
![Screen Shot 2021-06-20 at 4 51 37 PM](https://user-images.githubusercontent.com/60768642/122666384-cb191000-d1e7-11eb-8d98-8a4e155af984.png)

![Screen Shot 2021-06-20 at 4 53 21 PM](https://user-images.githubusercontent.com/60768642/122666418-09aeca80-d1e8-11eb-9b9f-d30f1c4789f3.png)


