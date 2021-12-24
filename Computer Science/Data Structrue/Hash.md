# 해시(Hash)
**Abstract**
  - 데이터를 효율적으로 관리하기 위해, 임의의 길이 데이터(input)을 고정된 길이의 데이터(key)로 매핑하는 것
  - 해시 함수를 구현하여 데이터를 해시 값으로 매핑

---
**사용 이유**
  - **적은 자원으로 많은 데이터를 효율적으로 관리** 하기 위함
  - 하드 디스트나 클라우드에 존재하는 무한한 데이터들을 유한한 개수의 해시값으로 매핑하면 적은 메모미로도 프로세스 관리가 가능해짐
  - input에 대해 언제나 동일한 Hash 값을 리턴, index를 알면 **빠른 데이터 검색** 이 가능해짐
  - 검색시 **해시 테이블의 시간 복잡도는 O(1)** (이진탐색트리는 O(logN)

---
**해시 충돌(Hash Collsion)**
  - 데이터가 많아지면, 다른 데이터에 대해 동일한 해시 값으로 충돌이 일어나는 현상(*비둘기집 원리*)

---
**해시 충돌(Hash Collision) 대처 방안**
  1. 체이닝(Chaining) : 연결리스트로 동일한 hash값을 찾는 노드를 계속 추가해나가는 방식(메모리 문제가 생길 수 있음)
  2. 개방주소법(Open Addressing) : 해시 함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장(새로운 키 값에도 데이터가 저장되어 있다면 다음 주소에 저장)  
      - 선형탐사 : 해시함수로 얻은 주소에서 다음 주소로 넘어가며 비어있는 주소를 탐색
      - 제곱탐사 : 해시함수로 얻은 주소에서 n^2만큼 다음주소로 넘어가서 비어있는 주소를 탐색
      - 이중해시 : 다른 해시 함수를 한 번 더 적용
      - 재해싱 : Hash Table의 크기를 리고, 새로운 Hash Table에 크기게 맞추어 모든 데이터를 다시 해싱, 상당한 비용 발생