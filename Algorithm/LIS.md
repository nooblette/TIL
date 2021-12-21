# 최장 증가 수열(Longest Increasing Sequence, LIS)
**Abstract**
  - 가장 긴 증가하는 부분 수열  
  - e.g.) [7, 2, 3, 8, 4, 5] => LIS는 [2, 3, 4, 5] 이고 길이는 4

---
**구현 방식 및 시간복잡도**
  - 동적계획법(DP) : O(n^2)
  - Lower Bound : O(nlogn)

---

## 동적계획법(Dynamic Programming, DP)을 이용한 접근
**Source Code**
  - DP
```c
int[] dp = new int[n]; // dp[x]는 x번째 수를 마지막 원소로 갖는 LIS의 길이

for(int i=0; i<n; i++){
  if(dp[i] == 0) dp[i] = 1;
  for(int j=0; j<i; j++){
    if(arr[j] < arr[i]){ // 1. 증가하는 부분이고
      if(dp[i] < dp[j]+1){ // 2. j가 아닌 다른 원소에 대해서 구한 LIS보다 arr[j]를 포함했을때 LIS가 더 길다면 갱신
        dp[i] = dp[j]+1;
      }
    }
  }
}
```

---

## Lower Bound를 이용한 접근
**Abstract**
  - 이분탐색을 이용하여 최적의 위치에다가 값을 삽입
  - 수열(*i*)을 처음부터(*i=0부터 n까지*) 확인(**O(n)**) + i 별로Lower Bound를 통해 최적의 위치 탐색(**O(logn)**)
  - **_O(nlogn)의 시간복잡도_**

---
**Process**
  1. LIS 배열의 가장 마지막 원소와 수열의 원소를 비교(LIS 배열의 default 값은 INF)  
  2-1. 배열의 가장 마지막 원소보다 현재 수열의 원소가 크다면 그대로 배열에 추가  
  2-2.  아니라면 lower bound를 통해 현재 수열의 원소가 들어갈 **최적의 위치**를 찾고 그 위치의 값과 원소를 교체 
  <br/>  
  ***최적의 위치***  
    - lower bound를 통해 배열의 원소중 수열의 원소(x)보다 *크거나 같은 값중 **최솟값*** 을 찾을 수 있음  
    - 이 **최적의 위치** 에 값을 x로 교환해줌으로써, LIS 배열의 원소를 가능한 많이 추가될 수 있는 상태로 유지할 수 있음  
    
---
**특징**
  - Lower bound로 구한 LIS 배열은 실제 LIS 값과 다를 수 있음(요소는 무관, **길이만 동일**)  
  *=>* 기존 수열상 뒤에 있던 원소에 대해 Lower bound로 구한 최적의 위치가 먼저 LIS 배열에 들어온 원소보다 앞에 들어올 수도 있기 때문  
  쉽게 말해, Lower Bound로 구한 LIS 배열의 원소에 순서는 기존 배열의 순서와 무관하다
  
---
**Source Code**
```c
int size = 0;
for(int i = 1; i <= n; i++){
  if(LIS[size] < arr[i]){
    LIS[size++] = arr[i];
  }
  else{
    int idx = LowerBound(LIS, 1, size, arr[i]);  // arr[i]가 들어갈 수 있는 최적의 위치(idx)를 찾음
    LIS[idx] = arr[i];
  }
}
```
```c
static int LowerBound(int[] LIS, int l, int r, int val){
  int mid = 0;
  int ans = 0;
  
  // val보다 크거나 같은 값중 최솟값이 되는 idx를 찾는다.
  while(l<=r){
    mid = (l+r)/2;
    if(LIS(mid)>=val){
      r = mid-1;
      ans = mid;
    }
    else{
      l = mid + 1;
    }
  }
  return ans;
}
```

    
    
