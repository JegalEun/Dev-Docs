# Queue

## Queue란?
큐(Queue)는 선입선출 `FIFO(First In First Out`구조로 저장하는 형식을 말한다. 즉, 먼저 들어온 데이터가 먼저 나가는 구조로 되어있다.

예를 들자면 가게에 줄을 생각하면 쉽다. 먼저 줄 선 사람이 먼저 나갈 수 있다. `Stack(LIFO)`과는 반대되는 개념이다.

<img width="731" alt="큐의 구조" src="https://user-images.githubusercontent.com/43868540/145669342-1b7f2d44-8acf-40de-adc6-d2f5c6130f96.png">

큐는 위와 사진과 같이 한쪽 끝`(Rear)`에서는 `삽입(Enqueue)`연산만 이루어지며 다른 한쪽`(Front)`에서는 `삭제(Dequeue)`연산만 이루어진다.

스택은 삽입/삭제가 한 곳에서 일어나 Top이라는 변수가 하나가 필요하지만, 큐는 삽입/삭제가 다른 곳에 일어나기 때문에 두 개의 변수가 필요하다.

## Queue의 연산
- `Enqueue()` : 맨 뒤(Rear)에 새로운 요소를 추가한다.
- `Dequeue()` : 맨 앞(Front)에 요소를 꺼낸다. 

## 선형 큐
지금까지 위에서 보여드린 큐가 선형큐다.

데이터가 증가하면 `Rear`의 값이 증가하고 그 위치에 데이터를 저장하게 된다. 삭제할 때는 `Front`의 값을 하나 증가하고 그 위치에 있는 데이터를 삭제하면 된다.

하지만 **선형큐의 문제점**이 있다.

`Front`와 `Rear`의 값이 계속 증가하기 때문에 배열의 끝에 도달하게 되면 배열 앞쪽에 값이 비어있어도 그 이후로 값을 추가하지 못한다. 따라서 배열의 요소를 주기적으로 비어있는 배열로 이동해야지만 데이터 추가가 가능하다. 

## 원형 큐
선형 큐의 이러한 문제점을 보완하기 위한 것이 원형 큐이다. 

큐를 **원형**으로 생각하여 `Front`와 `Rear`의 값이 배열의 끝에 도달하면 다음에 증가되는 값은 0이 되도록 하는 방식이다. 배열의 **처음과 끝이 연결**되어 있다는 것이다.

하지만 큐가 비어 있는 상태와 꽉 차있는 상태에는 Rear와 Front값이 0이 된다. 둘 상태를 구분하기 위해 값을 추가할 때 0번째부터 채우는 것이 아닌 1번째부터 값을 채우면 구분이 된다. 

<img width="700" alt="원형 큐" src="https://user-images.githubusercontent.com/43868540/145669985-1bce9686-846a-4e23-ac45-1a0e895af2cc.png">

## 큐의 활용예시
- 은행 업부
- 콜센터 고객 대기시간
- 우선순위가 같은 작업 예약(프린터의 인쇄 대기열)
> 대기순서가 있을 때 사용된다.

## 큐 구현
다음 코드는 **백준의 10845 큐** 문제를 따라 구현하였다.
``` java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class BOJ10845 {
	
	static int front=0;
	static int back=0;
	static int size=0;
	static int [] queue;

	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		StringBuilder sb = new StringBuilder();
		
		int num = Integer.parseInt(br.readLine());
		
		queue = new int[num];
		int top=-1;
		
		for(int i=0;i<num;i++) {
			st=new StringTokenizer(br.readLine());
			
			switch(st.nextToken()) {
			case "push" :
				push(Integer.parseInt(st.nextToken()));
				break;
			case "pop" :
				sb.append(pop()).append('\n');
				break;
			case "size" :
				sb.append(size()).append('\n');
				break;
			case "empty" :
				sb.append(empty()).append('\n');
				break;
			case "front":
				sb.append(front()).append('\n');
				break;
			case "back":
				sb.append(back()).append('\n');
				break;
			}
		}
		System.out.println(sb);

	}
	
	public static void push(int num) {
		queue[back++]=num;
		if(back>=queue.length) {
			back=0;
		}	
		size++;
	}
	
	public static int pop() {
		if(back==front) {
			return -1;
		}else {
			int data = queue[front];
			front++;
			
			if(front>=queue.length) {
				front=0;
			}
			
			size--;
			return data;
		}
	}
	public static int size() {
		return size;
	}
	
	public static int empty() {
		if(size==0) {
			return 1;
		}else {
			return 0;
		}
	}
	
	public static int front() {
		if(size==0) {
			return -1;
		}else {
			return queue[front];
		}
	}
	
	public static int back() {
		if(size==0) {
			return -1;
		}else if(back==0) {
			return queue[queue.length-1];
		}else {
			return queue[back-1];
		}
	}
}
```

----
#### Reference
- [큐의 활용](https://seill.tistory.com/576)
- [Queue](https://minosaekki.tistory.com/11)