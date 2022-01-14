# DFS(깊이 우선 탐색)

## 그래프 탐색
그래프 탐색이란 하나의 정점으로부터 시작해 차례대로 모든 정점들을 한 번씩 방문하는 것이다.

그래프 탐색에는 DFS, BFS가 있다. 이 외에도 다익스트라, 플로이드 와샬이 있다.

## 깊이 우선 탐색(DFS, Depth-First Search)
깊이 우선 탐색이란 로트(또는 특정) 노드에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법이다.

예를 들어서 미로를 탐색할 때 한 방향으로 갈 수 있을 때 까지 계속 가다가 더 이상 갈 수 없으면 다시 갈림길로 돌아가 다른 길을 찾아서 가는 것처럼 DFS도 마찬가지이다.

## DFS 특징
- 넓게 탐색하기보다는 깊게 탐색하는 것이다.
- 모든 노드를 방문하고자 할 때 이 방법을 선택한다.
- 깊이 우선 탐색(DFS)가 너비 우선 탐색(BFS_보다 좀더 간단하다.
- 검색 속도 자체는 너비 우선 탐색(BFS)보다 느리다.
- 어떤 노드를 방문했었는지 여부를 반드시 검사해야한다. 이를 검사하지 않을 경우 무한루프에 빠질 위험이 있다.
- 부모노드로 되돌아 가기 위해 **백트래킹**을 사용한다.

## DFS의 원리
<img width="1048" alt="DFS" src="https://user-images.githubusercontent.com/43868540/149466540-8572f1c2-7141-4fcb-9cf9-558c92876544.png">

> [출처](https://bbangson.tistory.com/42) 

## DFS의 구현
DFS를 구현하기 위해서는 **스택**을 이용하는 방법과 **재귀 호출**를 이용한 방식이 있다.

하지만 나는 재귀 호출를 이용한 방식을 익혀보고자 한다.

### 재귀 호출 이용한 DFS 구현
```java
static void dfs(int i) {
		visited[i]=true;
        // 방문했다고 표시(무한루프 방지)
		sb.append(i+" ");
		
		for(int j=1;j<=n;j++) {
			if(!visited[j] && map[i][j]==1) {    
                // 방문하지 않았고 간선이 있으면
				dfs(j);
			}
		}
	}
```

## 너비 우선 탐색 (BFS, Breadth-First Search)
깊이 우선 탐색(DFS)와 다르게 너비 우선 탐색(BFS)은 최대한 **넓게** 이동한 다음, 더이상 갈 수 없을 때 아래로 이동한다.

루트 노드(또는 특정)노드에서 시작해서 인접한 노드를 먼저 탐색하는 방법으로, 시작 정점으로부터 **가까운 정점을 먼저 방문**하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회방법이다. 

## BFS의 특징
- 재귀적으로 동작하는 DFS와 달리 **큐**를 사용하여 동작한다.
- 깊게(Deep) 탐색하기 전에 넓게(Wide) 탐색한다.
- 주로 두 노드 사이의 최단 경로를 찾고 싶을 때 이 방법을 선택한다. 
> 깊이 우선 탐색의 경우 모든 경로를 다 살펴봐야하지만 너비 우선 탐색의 경우 가까운 경로부터 탐색하기 때문에

## BFS의 원리
![99960F405BD01A8D18](https://user-images.githubusercontent.com/43868540/149468085-63473ee3-5cf4-4fe0-bde1-ab9f552181d5.png)

> [출처](https://bbangson.tistory.com/42)

## BFS의 구현
BFS를 구현하기 위해서는 **큐**를 이용한다.

```java
static void bfs(int i) {
		Queue<Integer> queue = new LinkedList<Integer>();
		visited[i]=true;
        // 방문했다고 표시
		queue.offer(i);
		
		while(!queue.isEmpty()) {
			int temp=queue.poll();
			
			sb.append(temp+" ");
			
			for(int j=1;j<=n;j++) {
				if(!visited[j] && map[temp][j]==1) {
					visited[j]=true;
					queue.add(j);
				}
			}
		}
	}
```

## DFS와 BFS 활용한 문제
- 그래프의 모든 정점을 방문하는 것이 주요한 문제
> DFS, BFS 두 가지 중 어느 것을 사용해도 상관없다.

- 경로의 특징을 저장해둬야 하는 문제
> 예를 들면 각 정점에 숫자가 적혀있고, a부터 b까지 가는 경로를 구하는데 경로에 같은 숫자가 있으면 안된다는 문제나 각각의 경로마다 특징을 저장해둬야 할 때는 DFS를 사용

- 최단거리를 구해야 하는 문제
> 최단거리 문제는 BFS가 유리하다. 왜냐하면 깊이 우선 탐색으로 검색할 경우 처음으로 발견되는 해답이 최단거리가 아닐 수 있지만, 너비 우선 탐색으로 현재 노드에서 가까운 곳부터 찾기 때문에 먼저 찾아지는 해답이 곧 최단거리이기때문이다. 

---- 
#### Reference 
- [DFS](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
- [DFS(2)](https://velog.io/@sohi_5/algorithmDFS)
- [DFS & BFS](https://devuna.tistory.com/32)
