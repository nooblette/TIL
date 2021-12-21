# 계수 정렬(Counting Sort)
**Abstract**
  - Comparision Sort 알고리즘과 달리 **계수정렬**과 **기수정렬**을 이용하면 *O(n)*의 시간복잡도로 문제 해결 가능
  - Counting이 필요
  - 정렬하는 숫자가 특정 범위 내에 있을때 유용(범위만큼 추가적인 메모리를 할당하는데 범위가 너무 크다면 부담이 된다)
  - e.g.) [100, 0, 100, 300]을 정렬한다면 추가적인 배열의 크기를 원소의 최댓값인 200으로 잡아야한다. 
___
**Process**
  e.g.) [5 5 3 4 5 1 0 4 1 3 0 2 4 2 3 0] 을 정렬
  1. 숫자별 등장 횟수를 count
|숫자|0|1|2|3|4|5|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|등장횟수|3|2|2|3|3|3|

| 값 | 의미 | 기본값 |
|---|:---:|---:|
| `static` | 유형(기준) 없음 / 배치 불가능 | `static` |
| `relative` | 요소 자신을 기준으로 배치 |  |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |  |
| `fixed` | 브라우저 창을 기준으로 배치 |  |

**비교 정렬 알고리즘의 한계**
![ComparsionSortDevisionTreeModel](./images/ComparsionSortDevisionTreeModel.jpg)
  - n개의 원소에 대한 결정 트리 모델에서 Leaf node는 총 n!개 존재한다.
  - 즉, Six-Comparision Sort는 아무리 빠른 알고리즘일지라도 Leaf node까지 도달하는데 log(n!)(=nlogn)만큼의 시간이 걸린다.
  - 이러한 O(nlogn)을 줄일 수 있는 방법은 Comparision을 하지 않는 것  
  **_=> 계수 정렬(Counting Sort), 기수 정렬(Radix Sort)_**
