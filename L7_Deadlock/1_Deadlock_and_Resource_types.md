# 교착상태
## Deadlock
![](https://images.velog.io/images/langssi/post/9f69adad-7432-47e9-ba92-606b69345e9b/image.png)
- 어느 프로세서도 자기가 원하는 자원을 가져갈 수 없음 

### Blocked/Asleep State
- 프로세스가 특정 이벤트를 기다리는 상태
- 프로세스가 필요한 자원을 기다리는 상태

### Deadlock State
- 프로세스가 **발생 가능성이 없는** 이벤트를 기다리는 경우
  - 프로세스가 deadlock 상태에 있음
- 시스탬 내에 deadlock에 빠진 프로세스가 있는 경우
  - 시스템이 deadlock 상태에 있음
  
계속 일을 못하는 상태 -> starvation과 유사해보임

### Deadlock vs Starvation
- Deadlock은 sleep 상태에서 존재, **자원**을 기다림
- 발생 가능성이 없음
![](https://images.velog.io/images/langssi/post/656d7f33-9519-451e-8989-c01f92b7467b/image.png)
- starvation은 프로세서(cpu)를 기다리는 상태
- 발생하는 이벤트이지만 우선순위에 밀려서 계속 기다리는 현상
![](https://images.velog.io/images/langssi/post/95d1c0b6-0f12-456d-ba26-3c989017d824/image.png)

## 자원의 분류
### 일반적 분류
- Hardware Resources vs Software Resources
### 다른 분류 법(deadlock의 관점)
- 선점 가능 여부에 따른 분류
- 할당 단위에 따른 분류
- 동시 사용 가능 여부에 따른 분류
- 재사용 가능 여부에 따른 분류

## 선점 가능 여부에 따른 분류
### Preemption Resources
- Preemptible: 다른 쪽에서 내가 쓰는 자원을 뺏어갈 수 있다.
- 선점 당한 후, 돌아와도 문제가 발생하지 않는 자원
- Processor(saving, restoring), Memory(swap device) 등
### Non-preemptible Resources
- 선점 당하면 이후 진행에 문제가 발생하는 자원
  - Rollback, Restart등 특별한 동작이 필요
    - ![](https://images.velog.io/images/langssi/post/e6462639-d27b-4711-b3cf-064376cd58c2/image.png)
    - 여권을 아들에게 선점 당함 -> write operation
- E.g., disk drive 등

## 할당 단위에 따른 분류
### Total Allocation Resources
- 자원 전체를 프로세스에게 할당
- E.g., Processor, Disk Drive 등 -> 한번에 하나의 프로세스만 사용 가능

### Partitioned Allocation Resources
- 하나의 자원을 여러 조각으로 나누어, 여러 프로세스들에게 할당
- E.g., Memory 등

## 동시 사용 가능 여부에 따른 분류
### Exclusive Allocation Resources
- 한 순간에 한 프로세스만 사용 가능한 자원
- E.g., Processor, Memeory(본인에게 할당된 영역은 본인만 쓸 수 있다), Disk Drive 등
### Shared Allocation Resource
- 여러 프로세스가 동시에 사용 가능한 자원
- E.g., Program(sw) - 소스코드, exe 파일 등... , shared data 등  

## 재사용 가능 여부에 따른 분류
### SR(Serially-uesable Resources)
- 시스템 내에 **항상 존재**하는 자원
- 사용이 끝나면 다른 프로세스가 사용 가능
- E.g., Processor, Memory, Disk Drive, Program 등
### CR(Consumable Resources)
- 한 프로세스가 사용한 후에 사라지는 자원
- E.g., signal, message 등 (받으면 사라짐)
## Deadlock과 자원의 종류
### Deadlock을 발생시킬 수 있는 자원의 형태
- Non-preemptible Resources
  - 자원을 한번 할당받으면 게속 쓰기 때문에 다른 프로세스에서 요청을 하면 자원이 계속 할당되지 않으므로
- Exclusive Allocation Resources
- Serially Reusable Resources
- 할당 단위는 영향을 미치지 않음
  - 혼자 쓴다고 해도 preemptible하다면 문제되지 않음

### CR을 대상으로 하는 Deadlock Model
- 사라진 자원을 기다리고 있는 프로세서가 있었다면 deadlock이 발생 할수도 있지만...
- 이것까지 고려하면 너무 복잡하므로 serially reusable process로만 생각한다.
