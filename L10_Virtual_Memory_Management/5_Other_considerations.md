# Other Considerstaions
- Page size
- Program restructuring
- TLB reach

## 1. Page Size
- 일반적인 page size
    - <img width="300" alt="스크린샷 2021-06-12 오후 5 49 05" src="https://user-images.githubusercontent.com/70195733/121770822-a0570800-cba6-11eb-9a03-96ac24e884f5.png">
    
#### Small page size
- Page Table이 크다. (오버헤드 큼)
- 내부 단편화 감소
- I/O 시간 증가
- Locality 향상
- Page fault 증가
#### Large page size
- page table이 작다. (오버헤드 작음)
- 내부 단편화 증가
- I/O시간 감소
- Locality 저하
- Page fault 감소

#### 페이지 크기는 클수록 좋은걸까? 아니면 작을수록 좋은걸까?
- No best Answer
- 하지만 요즘은 페이지 크기가 점점 커지는 추세다.  이유는?
    - HW의 발전 경향과 연관이 있다.
    - CPU 성능도 증가하고 메모리 사이즈도 등가하는 추세.
    - 메모리 속도 보다 CPU 속도의 증가가 압도적이기 때문에, I/O를 최소화하는게 좋다.(I/O많으면 CPU가 메모리 기다리느라 병목현상 생김)
    
## 2.Program restructuring
- 가상 메모리 시스템의 특성에 맞도록 프로그램을 재구성
- 사용자가 가상 메모리 관리 기법(예, paging system)에 대해 이해하고 있다면, 프로그램의 구조를 변경하여 성능을 높일 수 있음
- 예를 들어 이중 for loop을 비효율 적으로 도는 아래 코드를 수정하며 성능을 개선할 수 있다.
<img width="1357" alt="스크린샷 2021-06-12 오후 5 57 28" src="https://user-images.githubusercontent.com/70195733/121770994-b3b6a300-cba7-11eb-88ba-4df7d02e6a4c.png">
<img width="1022" alt="스크린샷 2021-06-12 오후 5 57 42" src="https://user-images.githubusercontent.com/70195733/121770997-b87b5700-cba7-11eb-85d1-b1709eb60a45.png">

## 3.TLB reach
- Direct Address Mapping 할 때 느린 속도의 한계를 개선하기 위해 두는 HW.
#### TLB Reach란?
    - TLB를 통해 접근할 수 있는 메모리의 양
    - the number of entries \* the page size
    
#### TLB의 Hit ratio를 높이려면?
- TLB 크기 증가
    - Expensive
- Page 크기 증가 or 다양한 page size 지우너
    - OS의 지원이 필요
