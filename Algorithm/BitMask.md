# 비트마스크(BitMask)

**Abstract**
  - 집합을 구성하는 요소들을 표현할때 유용한 테크닉

---
**사용하는 이유**
  - DP, 순열 등 배열 만으로는 활용할 수 없을때 **(n이 너무 클 때)**
  - 원소의 수가 너무 많지 않다면 적은 메모리와 빠른 수행시간으로 해결 가능
  - 집합을 **배열의 인덱스** 로 표현, 코드가 간결

e.g) {1, 2, 3, 4, 5}라는 집합의 부분집합을 표현
방법 1. loop를 돌려가며 배열에 저장하여 경우의 수를 구할 수 있음
방법 2. 비트 마스킹을 통해 **효율적으로** 표현 가능

| 부분집합 | 비트마스킹 | 10진법 |
|:---:||:---:|:---:|
| {1, 2, 3, 4, 5} | 11111 | 31 |
| {2, 3, 4, 5} | 11110 | 30 |
| {1, 2, 5} | 10011 | 19 |
| {2} | 00010 | 2 |

***=>* (비트마스킹한 값을 다시 10진법으로 표현도 가능)**

---
**비트 연산**
  부분집합에 i를 추가하고 싶다면 i번째 bit를 1로 바꿔주는 것만으로 표현 가능(A, B는 비트로 표현된 값)
  - AND(A&B) : 두 비트가 모드 1일때 1을 반환
  - OR(A|B) : 두 비트중 하나라도 1이면 1을 반환
  - XOR(A^B) : 두 비트가 서로 다르다면 1을 반환
  - NOT(A~B) : 비트를 반전(1->0 or 0->1)
  - SHIFT(A>>B, A<<B) : 오른쪽(A/2^B)으로 혹은 왼쪽(A*2^B)으로 이동 

---
**활용**
  1. 삽입 -> **OR연산**  
    e.g) *10101* 에서 3번째 비트를 1로 바꾸고 싶다면  
    10101 **|** *1<<3* ➡️ 10101 **|** *01000* ➡️ **11101**  
    
  2. 삭제 -> **AND연산과 NOT연산**  
    e.g) *11101* 에서 3번째 비트를 0으로 바꾸고 싶다면  
    11101 **&** *~1<<3* ➡️ 11101 **&** *~01000* ➡️ 11101 **&** *10111* ➡️ **10101**  
    
  3. 조회 -> **AND연산**  
    e.g) *10101* 에서 3번째 비트를 1로 바꾸고 싶다면   
    10101 **&** *1<<3* ➡️ 10101 **&** *01000* ➡️ **01000** 
    <br/>  
    e.g) *10101* 에서 4번째 비트를 1로 바꾸고 싶다면  
    10101 **&** *1<<4* ➡️ 10101 **&** *10000* ➡️ **10000**