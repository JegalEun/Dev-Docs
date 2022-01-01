# 백트래킹 (Backtracking)

## 백트래킹
순열 문제를 풀다가 **백트래킹**이라는 개념이 나와서 정리를 하게 되었다.

백트래킹은 **알고리즘 기법** 중 하나로, 해를 찾는 도중 더이상 탐색을 진행할 수 없는 상황이면 되돌아가서 다시 해를 찾아가는 기법을 말한다. 

<img width="693" alt="백트래킹 실행" src="https://user-images.githubusercontent.com/43868540/147810580-b79ca693-664f-4195-9189-d5b55e93870e.png">

> [출처](https://iseunghan.tistory.com/241)

## DFS와 백트래킹

### 깊이 우선 탐색(DFS)
DFS는 가능한 **모든 경로를 탐색**한다. 따라서 불필요할 것 같은 경로를 사전에 차단하거나 하는 등의 행동이 없으므로 경우의 수를 줄이지 못한다.
따라서 **비효율적**인 결과를 초래할 수 있다.

### 백트래킹(Backtracking)
백트래킹은 DFS의 비효율적인 경로를 차단한다는 점에서 다른 특징을 가진다. 해를 찾는 도중, 지금의 경로가 해가 될 것 같지 않으면 그 경로를 더이상 가지 않고 되돌아간다. 

즉, 코딩에서는 반복문의 횟수를 줄일 수 있어 시간을 단축하여 **효율적**이다. 

이를 **가지치기**라고 하는데, 불필요한 부분을 쳐내고 최대한 올바른 쪽으로 간다는 의미이다. 

정리하자면, 백트래킹은 모든 가능한 경우의 수 중에서 **특정한 조건을 만족하는 경우**만 살펴보는 것이다. 

주로 문제 풀이에서는 DFS 등으로 모든 경우의 수를 탐색하는 과정에서 조건문 등 답이 될 수 없는 상황을 정의하고 이러한 상황에 맞닥뜨리면 그 이전으로 돌아가서 다른 경우를 탐색한다.

## 백트래킹 문제
### N과 M(1) 풀어보기
자연수 N이 주어지면 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열을 출력한다. 

`i=1`일때, 1을 방문했다(true)고 표시한 뒤, 다음 1을 방문했을 때 이미 1을 방문했으므로 넘어간다.

`i=2`일때, visited[2]=false 이므로 방문한다. 

<img width="577" alt="백트래킹 순서" src="https://user-images.githubusercontent.com/43868540/147851649-9cb90df4-318a-43a3-9fb5-1dca45f94706.png">

<img width="577" alt="백트래킹 순서" src="https://user-images.githubusercontent.com/43868540/147851672-850aa3cd-473d-41a2-820b-c0ceb6429835.png">

> [출처 iseunghan.tistory](https://iseunghan.tistory.com/241)

그리고 `i=3`일때, visited[1], visited[2]는 true이고 visited[3]=false 이기때문에 visited[3]을 방문한다. 

그 후, 재귀 호출할 때 넘겨주는 depth가 M과 같아 지는 시점에 출력을 한다. 

지금 현재 `i=3`이다. 그리고 더 이상 해를 구할 수 없기 때문에 3을 종료한 후에는 visited[3]을 false로 바꾸어주고 2를 종료한 후에는 visited[2]를 false로 바꿔줘야 한다.

<img width="574" alt="백트래킹" src="https://user-images.githubusercontent.com/43868540/147851995-49a47c67-91bd-4006-820f-9c3c52d432a7.png">

> [출처 iseunghan.tistory](https://iseunghan.tistory.com/241)

<img width="574" alt="백트래킹" src="https://user-images.githubusercontent.com/43868540/147852159-7fdae619-476e-46b4-8c26-7891b10a5350.png">

> [출처 iseunghan.tistory](https://iseunghan.tistory.com/241)

그리고 다시 visited[3]=true로 체크하고 depth(2)에 i값인 3을 넣어준다.

<img width="607" alt="백트래킹" src="https://user-images.githubusercontent.com/43868540/147852195-4c2dc708-17fd-4b93-a08e-94441682075f.png">

> [출처 iseunghan.tistory](https://iseunghan.tistory.com/241)

그러면 visited[1]=visited[3]=true, visited[2]=false가 된다.
따라서 visited[2]를 true로 바꿔주고 `1->3->2` 로 방문한다.

그러면 `depth==3`이 되어 출력한다.

여기까지 앞자리가 `1`인 수열 `1,2,3`, `1,3,2`을 출력하였다. 이것을 반복해서 2,3,4 ... 까지 반복하면 된다. 

## 전체 코드 
``` java
package Week05;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class BOJ15649 {

	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder(); 
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int n = Integer.parseInt(st.nextToken());
		int m = Integer.parseInt(st.nextToken());
		
		int arr[]=new int[n];
		int newArr[] = new int[n];		
		boolean visited[] = new boolean[n];
		
		for(int i=0;i<n;i++) {
			arr[i]=i+1;
		}
		
		nm(arr, newArr, visited, 0, n, m);
		
		
	}
	
	static void nm(int arr[], int newArr[], boolean visited[], int depth, int n, int m) {
		
		for(int i=0;i<n;i++) {
			if(depth==m) {
				print(newArr, m);
				return;
			}else {
				if(!visited[i]) {
					visited[i]=true;
					newArr[depth]=arr[i];
					nm(arr, newArr, visited, depth+1, n, m);
					visited[i]=false;
				}
			
			}
		}
	}
	static void print(int newArr[], int m) {
		for(int i=0;i<m;i++) {
			System.out.print(newArr[i]+" ");
		}
		System.out.println();
	}

}
```

----
#### Reference
- [백트래킹의 정의 및 예시 문제](https://chanhuiseok.github.io/posts/algo-23/)
- [백트래킹 순서](https://iseunghan.tistory.com/241)

