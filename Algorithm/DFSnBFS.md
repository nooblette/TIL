# 깊이 우선 탐색(DFS) & 너비 우선 탐색(BFS)

-   그래프 혹은 트리에서 **경로를 탐색하는 2가지 방법**

---

## **깊이 우선 탐색(DFS)**

\- 한 node에서 **다음 브랜치로 넘어가기 전에, 해당 브랜치를 모두 탐색**하는 방법  
\- **모든 경로를 방문**해야 할때 적합  
\- _Stack_을 통해 현재까지 방문한 경로를 기록  
\- 한 node의 자식 노드를 모두 방문한 후, 그 node의 형제노드로 넘어가는 탐색 방식

---

**방문 순서**

[##_Image|kage@qkfte/btroxjiitZ8/Kbes6qI8zS60XGOCZgadNk/img.jpg|CDM|1.3|{"originWidth":638,"originHeight":586,"style":"alignCenter","width":297,"height":272,"filename":"./images/DFS.jpg"}_##]

---

**Process**

1.  한 node에서 연결된 다른 정점을 방문한다.
2.  다시 계속해서 방문할 수 있는 정점을 방문한다.
3.  더 이상 방문할 정점이 없다면 이전 정점으로 돌아가서 다른 정점을 방문한다.
4.  모든 노드를 방문할때까지 계속 반복

---

**_Source Code_**  
\- 인접행렬(adjacent matrix)로 구현

```
void dfs(int x){ // x는 현재 방문한 노드를 의미 
    check[x] = true; // 방문 여부를 저장 
    for(int i = 1; i <= n; i++){ 
        // x번 노드에서 i번 노드로 가는 경로가 존재하고, i번 노드를 방문한 적이 없다면
        if(graph[x][i] != 0 && !check[i]) { 
             dfs(i); // 계속해서 방문할 수 있는 정점을 반복(재귀호출) 
         } 
     } 
}
```

\- 인접리스트(adjacent list)로 구현

```
void dfs(int x){
    check[x] = true;
    for(int i = 0; i < adj_list[x].size(); i++){ // x번 노드에서 연결된 정점의 개수만큼
        if(!check(adj_list[x][i]) { // x번 노드에서 i번 노드로 가는 경로를 방문하지 않았다면
            dfs(adj_list[x][i]); // 다시 계속해서 방문
        }
     }
}
```

**\=> 경로 저장을 인접 행렬로 할 것인가, 인접 리스트로 할것인가의 차이이다**

---

**시간 복잡도**  
인접 행렬로 구현 시 : O(V^2)

-   모든 정점을 방문해야 하므로 dfs()는 n번 호출 => O(v)
-   연결정보를 검사하기 위해서 한 노드에서 모든 노드에 대해 연결 여부를 확인해야 하므로 => O(v\*v) = O(v^2)

인접 리스트로 구현 시 : O(V+E)

-   모든 정점을 방문해야 하므로 dfs()는 n번 호출 => O(v)
-   연결정보를 검사하기 위해 한 노드에서 연결된 간선의 개수만큼만 진행하면 되므로 => O(v+e)

_V : vertex(접점), E : Edge(간선)_

---

## **너비 우선 탐색(BFS)**

\- 한 node에서 **같은 브랜치에 있는 노드(형제 노드들)를 먼저 탐색**하는 방법  
\- _Queue_를 통해 어디를 방문할 것인지 기록  
\- 모든 경로를 탐색하는 것보다 **최소 비용을 구할때** 적합

---

**방문 순서**

[##_Image|kage@EtUFZ/btroxkuH29d/IW3PlVP9IsUbl7aatHszF0/img.jpg|CDM|1.3|{"originWidth":549,"originHeight":600,"style":"alignCenter","width":312,"height":341,"filename":"./images/BFS.jpg"}_##]

---

**Process**

1.  한 정점에서 연결된 모든 노드를 Queue에 삽입
2.   Queue에 정점 번호를 삽입한다면, 이 정점은 방문한 것으로 간주하고 check에 방문여부를 저장
3.  Queue에 가장 앞에있는 원소를 pop
4.  이 원소에 대해 다시 1번 과정을 Queue가 빌 때 까지 반복

---

**_Source Code_**  
\- 인접행렬(adjacent matrix)로 구현

```
void bfs(){
	queue<int> q;
    
    // 1번 노드부터 시작
    check[1] = ture;
    q.push(1);
    
    while(!q.empty()){
    	int x = q.pop();
        for(int i=1; i<=n; i++){
        	if (graph[x][i] != 0 && !check[i]){
            	check[i] = true;
                q.push(i);
            }
        }
    }
}
```

\- 인접리스트(adjacent list)로 구현

```
void bfs(){
	queue<int> q;
    
    // 1번 노드부터 시작
    check[1] = ture;
    q.push(1);
    
    while(!q.empty()){
    	int x = q.pop();
        for(int i=1; i<=adj_list[x].size(); i++){
        	if (!check[adj_list[x][i]){
            	check[adj_list[x][i]] = true;
                q.push(adj_list[x][i]);
            }
        }
    }
}
```

---

**시간 복잡도**

-   인접 행렬로 구현 시 : O(V^2)
-   인접 리스트로 구현 시 : O(V+E)
-   DFS와 이유는 동일!
