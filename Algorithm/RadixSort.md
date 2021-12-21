# 기수 정렬(Radix Sort)
**Abstract**
  - **데이터를 구성하는 기본요소(_Radix_)** 를 이용하여 정렬하는 방식
  - 안정정렬
___
**시간복잡도**
O(d*(n+b)) = O(n)  
d = 정렬할 숫자의 자릿수  
b = 10으로 고정(계수 정렬에서 k)  
___
**장점**
  - 문자열, 정수 정렬 가능
___
**단점**
  - 자릿수가 없는 것(e.g.) 부동 소수점)은 정렬할 수 없음
  - 중간결과를 저장할 bucket이 필요함
  - 입력이 모두 k 자릿수 이하의 자연수인 특수한 경우에서만 사용 가능
___
**Process**  
![RadixSortProcess](./images/RadixSortProcess.jpg)
- 각 자리수별로 정렬할때, **기존 비교정렬 알고리즘을 사용하는것이 아닌,**  **0~9까지 표시된 공간을 마련해서** 해당자릿수와 일치하는 원소를 저장  **_-> Comparision Sort보다 빠르게 만드는 요소_**
___
**낮은 자릿수부터 정렬하는 이유**  
_**MSD**(가장 큰 자릿수부터 Counting Sort) vs **LSD**(가장 낮은 자릿수부터 Counting Sort)_  
  - LSD
    - 모든 자릿수를 따져야함(e.g.) 1과 16000000을 비교한다면 00000001과 16000000으로 비교해야함)
    - 중간 정렬결과를 알 수 없음(e.g.) 10004와 70002를 비교) **->최대 자릿수까지 가봐야 정렬결과를 알 수 있음**
    - 자릿수가 정해진경우 MSD보다 조금 더 빠를 수 있음
    - 일관된 알고리즘 (이부분에 대해 어떤 요인으로 인해 일관되었다고 표현하는지 잘 모르겠다)  
  - MSD  
    - 중간에 정렬이 완료될 수 있고, 모든 자릿수를 따지지 않아도 됨 *-> LSD보다 빠름*  
    - 하지만 이때문에, 중간에 데이터를 점검해야함(메모리를 더 사용하게됨)  
    - 알고리즘이 일관되지 못함  
  
  **=> 이러한 이유로 *LSD*를 사용**
___
**Source Code**
```c
void CountSort(int[] arr, int n, int exp){ // 일반적인 계수 정렬
  int buffer[n];
  int i, count[10] = {0};
  
  // exp자릿수에 해당하는 Count 증가(e.g) exp = 10이면 10의 자릿수에 해당하는 수에 대해서만 계수정렬을 사용)
  for(i=0; i<n; i++){
    count[(arr[i]/exp)%10]++; // exp자릿수를 뽑아냄
  }
  
  // 누적합
  for(i=1; i<10; i++){
    count[i] = count[i-1];
  }
  
  // count[value]에 해당하는 값(value)를 buffer에 정렬되게 삽입을 진행
  for(i=n-1; i>=0; i--){
    buffer[count[(arr[i]/exp)%10)-1] = arr[i];
    count[(arr[i]/exp)%10]--;
  }
  
  for(i=0; i<n; i++){
    arr[i] = buffer[i];
  }
}
```
```c
void RadixSort(int[] arr, int n){
  int m = getMax(arr, n); // 최대값의 자릿수를 구함
  
  for(int exp=1; m/exp>0; exp*=10){ // 최댓값을 자릿수로 나눴을때 0이 나오면, arr의 모든 숫자가 exp보다 낮은 자릿수이므로 탐색 종료
    CountSort(arr, n, exp); // 각 자릿수별로 계수정렬 진행
  }
}
 ```
