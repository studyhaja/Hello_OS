### Replacement Strategies(교체 기법)
#### Fixed allocation
- MIN(OPT, B0) algorithm
- Random algorithm
- FIFO(First In First Out) algorithm
- LRU(Least Recently Used) algorithm
- LFU(Least Frequently Used) algorithm
- NUR(Not Used Recently) algorithm
- Clock algorithm
- Second change algorithm
#### Variable allocation
- WS(Working Set) algorithm
- PFF(Page Fault Frequency) algorithm
- VMIN(Variable MIN) algorithm


#### 지난번까지 Fixed allocation을 알아봤고, 이번 강의부턴 variable allocation을 공부합니다!


# Variable Allocation
- 할당하는 메모리의 크기가 가변적인 방법이다.
총 3가지 방법이 있다: WS(Working Set) algorithm, PFF(Page Fault Frequency) algorithm, VMIN(Variable MIN) algorithm

## 1. WS(Working Set) algorithm
- 1968년 Denning이 제안
- Working set
    - Process가 특정 시점에 자주 참조하는 page들의 집합
    - 최근 일정 시간(Δ)동안 참조된 page들의 집합
    - 시간에 따라 변함
    - W(t, Δ)
        - The working set of a process at time t
        - Time interval(t-Δ, t)동안 참조된 pages들의 집합
        - Δ: window size, system parameter
<img width="700" alt="스크린샷 2021-06-11 오전 10 18 39" src="https://user-images.githubusercontent.com/70195733/121616749-74e8f600-ca9e-11eb-84d4-15e3fa45713d.png">
<img width="700" alt="스크린샷 2021-06-11 오전 10 18 44" src="https://user-images.githubusercontent.com/70195733/121616809-921dc480-ca9e-11eb-81e6-6430cb77b319.png">
<img width="700" alt="스크린샷 2021-06-11 오전 10 18 47" src="https://user-images.githubusercontent.com/70195733/121616822-99dd6900-ca9e-11eb-89d1-075258adfcc8.png">
- Locality에 기반
- Working set을 메모리에 항상 유지
    - Page fault rate(thrashing) 감소
    - 시스템 성능 향상
- Window size(Δ)는 고정
    - Memory allocation은 가변
    - Δ값이 성능 결정 짓는 중요한 요소
<img width="600" alt="스크린샷 2021-06-11 오전 10 36 01" src="https://user-images.githubusercontent.com/70195733/121617916-d5793280-caa0-11eb-84ce-99070f600973.png">
- locality 때문에 윈도우가 커져도 working set사이즈 증가율이 감소하는 지점이 온다.(쓰는 것만 계속 쓰기 때문에.)
<img width="600" alt="스크린샷 2021-06-11 오전 10 37 58" src="https://user-images.githubusercontent.com/70195733/121618071-20934580-caa1-11eb-917e-6b70c7b93643.png">
<img width="600" alt="스크린샷 2021-06-11 오전 10 39 06" src="https://user-images.githubusercontent.com/70195733/121618136-43bdf500-caa1-11eb-8cea-985f825ae044.png">
<img width="600" alt="스크린샷 2021-06-11 오전 10 40 19" src="https://user-images.githubusercontent.com/70195733/121618297-87186380-caa1-11eb-9ca3-8bad2f752a6d.png">
<img width="600" alt="스크린샷 2021-06-11 오전 10 40 35" src="https://user-images.githubusercontent.com/70195733/121618368-9ac3ca00-caa1-11eb-8012-ad144ea4b32c.png">
<img width="600" alt="스크린샷 2021-06-11 오전 10 40 44" src="https://user-images.githubusercontent.com/70195733/121618449-bdee7980-caa1-11eb-8337-35051e9ebc42.png">
<img width="600" alt="스크린샷 2021-06-11 오전 10 40 58" src="https://user-images.githubusercontent.com/70195733/121618491-d199e000-caa1-11eb-96dd-72bff89f7743.png">

#### 성능 평가
- Page fault수 외 다른 지표도 함께 봐야 함
- Example
    - Time interval [1,10]
        - \# of page fault = 5
        - 평균 할당 page frame 수 = 3.2
    - 평가
        - 평균 3.2개의 page frame을 할당 받은 상태에서 5번의 page fault 발생
        
#### 특성
- 적재되는 page가 없더라도 메모리를 반납하는 page가 있을 수 있음
- 새로 적재되는 page가 있더라도, 교체되는 page가 없을 수 있음
#### 단점       
- Working set management overhead(윈도우 지속적으로 관찰해야 함)
- Residence set(상주 집합)을 page Fault가 없더라도 지속적으로 관리해야 함.
        
#### Mean number of frames allocated vs page fault rate
- window size가 증가하면 page fault는 감소하지만, 메모리 lifetime도 증가하기 때문에 page 유지비용이 증가한다.
- 이런 것들을 고려해서 적절한 지점을 잘 찾아야 한다.
<img width="500" alt="스크린샷 2021-06-11 오전 10 46 22" src="https://user-images.githubusercontent.com/70195733/121618721-45d48380-caa2-11eb-974a-83c1bd37550e.png">

## 2. PFF(Page Fault Frequency) algorithm
- Residence set size를 page fault rate에 따라 결정
    - Low page fault rate(long inter-fault time)
        - Process에게 할당된 PF 수를 감소
    - High page fault rate(short inter-fault time)
        - Process에게 할당된 PF 수를 증가
- Resident set 갱신 및 메모리 할당
    - Page fault가 발생시에만 수행
    - Low overhead
#### Criteria for page fault rate
- IFT > τ('타우' 라고 읽는다): Low page fault rate
- IFT < τ: High page fault rate
- τ: threshold value
    - System parameter
- IFT: Inter Fault Time(페이지 폴트간의 시간 간격)

#### Algorithm
<img width="600" alt="스크린샷 2021-06-11 오전 11 20 58" src="https://user-images.githubusercontent.com/70195733/121621446-22f89e00-caa7-11eb-8122-f54761aae902.png">
## 3. VMIN(Variable MIN) algorithm

#### Example
<img width="700" alt="스크린샷 2021-06-11 오전 11 26 39" src="https://user-images.githubusercontent.com/70195733/121621866-f5f8bb00-caa7-11eb-898c-46eed66c3c0f.png">


#### 성능 평가
- 평균 3.7개의 page frame을 할당 받은 상태에서 5번의 page fault 발생

#### 특징
- 메모리 상태 변화가 page fault 발생 시에만 변함
    - Low overhead
    
    
## 3. Variable MIN(VMIN) algorithm
- Optimal algorithm(최적의, 이상적인, 구현 불가능한)
    - 평균 메모리 할당량과 page fault 발생 횟수 모두 고려했을 때의 Optimal
- 실현 불가능한 기법(Unrealizable)
    - Page reference string을 미리 알고 있어야 함
- 기법
    - \[t, t+ Δ\]을 고려해서 교체할 page 선택
    
#### Algorithm
- Page r이 t 시간에 참조 되면, Page r이 (t, t+ Δ) 사이에 다시 참조되는지 확인
- 참조 된다면, page r을 유지
- 참조 안 된다면, apge r을 메모리에서 내림

#### Example
<img width="600" alt="스크린샷 2021-06-11 오전 11 32 23" src="https://user-images.githubusercontent.com/70195733/121622293-b7173500-caa8-11eb-89e4-41fb7017bd0a.png">

#### 성능 평가
- 평균 1.6개의 page frame을 할당 받은 상태에서 5번의 page fault 발생

#### 최적 성능을 위한 Δ값
<img width="600" alt="스크린샷 2021-06-11 오전 11 34 08" src="https://user-images.githubusercontent.com/70195733/121622449-fba2d080-caa8-11eb-9887-eb828a6a47d0.png">
