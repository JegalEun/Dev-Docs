# Stack
스택은 자료구조를 공부하는데 가장 기본적인 개념이다. 

## stack이란
스택은 **후입선출**이라 불리며 `LIFO(Last In First Out)`의 형태를 보인다.
즉, 가장 나중에 들어간 데이터가 먼저 나온다. 

스택은 들어가는 대로 차곡차곡 쌓여서 나갈 때는 역순으로 빠져나가는 자료형이다. 

상자를 생각하면 쉽다. 상자 안에 책을 넣으면 가장 나중에 넣은 책이 제일 맨위로 오게된다. 만약, 제일 아래에 있는 책을 빼려면 모든 책을 꺼내야 한다.

<img width="314" alt="스택의 구조" src="https://user-images.githubusercontent.com/43868540/145668135-9e7c81e5-8bc9-40ad-9cc1-272692036dc1.png">

> [출처 위키피디아](https://ko.wikipedia.org/wiki/스택)

## Stack의 연산
- `push()` : 스택의 가장 마지막 자리(top) 위에 메모리를 생성하고 데이터 x를 넣는다. 
- `pop()` : 스택의 가장 윗 데이터를 빼고 삭제한다. push와 마찬가지로 마지막 위치(top)에서 삭제한다.  
- `top()` : 스택의 가장 윗 데이터를 반환한다. 만약 스택이 비었다면 -1을 반환한다. 
- `empty()` : 스택이 비었는지 확인하는 연산. 스택이 비었다면 1을 반환하고,그렇지 않다면 0을 반환한다.

## Stack의 활용 예시
- 웹 브라우저 방문기록 : 가장 나중에 열린 페이지부터 보여준다.
- 역순 문자열 만들기 : 가장 나중에 입력한 문자열부터 보여준다.
- 실행취소(undo) : 가장 나중에 실행된 것부터 취소한다.
- 후위표기법 계산

## Stack의 장점
- 구조가 단순해서 **구현이 쉽다.**
- 데이터의 **저장/읽기 속도가 빠르다.**

## Stack의 단점
- 데이터의 최대 개수를 미리 정해야한다.
- 따라서 스택공간을 다 사용하지 않을 경우 저장공간의 낭비로 이어질 수 있다.

## 구현
다음 코드는 **백준의 10828번 스택**에 관한 코드이다.
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class BOJ10828 {

	static int top =-1;
	static int [] stack;      // 스택 배열 생성
	
	public static void main(String[] args) throws IOException {
		
		
		// TODO Auto-generated method stub
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		
		int num = Integer.parseInt(br.readLine());
		stack = new int[num];
		
		StringTokenizer st = null;
		
		for(int i=0;i<num;i++) {
			st = new StringTokenizer(br.readLine(), " ");
			
			switch(st.nextToken()){
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
			case "top" :
				sb.append(top()).append('\n');
				break;
			}
		}
		
		System.out.println(sb);
	}
	
	public static void push(int num) {
		top++;                  // 데이터의 마지막 위치(top)를 하나 증가시킨다.
		stack[top]=num;         // 증가시킨 빈 배열에 push한다.
	}
	
	public static int pop() {
		if(top==-1) {               // 배열에 아무것도 없다면 -1 반환
			return -1; 
		}else {
			int num = stack[top];     //배열의 마지막 원소를 반환하고 top--
			top--;
			return num;
		}
	}
	
	public static int size() {
		return top+1;               //배열의 크기는 배열의 마지막 위치 반환 (top이 -1로 시작했기때문에 +1)
	}
	
	public static int empty() {
		if(top==-1) {               //비어있다면 1 반환. 아니면 0반환
			return 1;
		}
		else {
			return 0;
		}
	}
	
	public static int top() {
		if(top==-1) {               //top이 -1이면 배열에 아무것도 없는 상태
			return -1;
		}
		else {
			return stack[top];        //배열의 마지막 원소 반환
		}
	}
}
``` 

----
#### Reference
- [스택](https://ko.wikipedia.org/wiki/스택)
- [스택의 활용예시](https://devuna.tistory.com/22)
- [스택의 장단점](https://onnons.tistory.com/293)
