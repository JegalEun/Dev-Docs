# React
우아한테크러닝을 들으면서 `React`에 대해 배우면서 기초적인 지식이 기반이 필요한 것 같았다.

`React` 이름만 들어봤기때문에 이해하고 따라가는데에 벅찬 느낌이 들어 이번 기회에 공부해보았다.

## React란?
`React`는 페이스북에서 만든 사용자 UI 구축을 위한 자바스크립트 라이브러리이다. 현재 웹/앱 `view`를 만들기 위해서 사용되는 가장 인기있는 라이브러리다.
> 자바스크립트 라이브러리란 동적인 웹 페이지를 보다 효율적으로 유지 보수하고 관리할 수 있도록 하는 라이브러리이다.

그렇다면 왜 `React`를 사용하냐?

단순한 정적 페이지를 만드는 것이 목적이라면 `React`와 같은 자바스크립트 라이브러리는 필요없지만 요즘 웹 페이지는 동적으로 만들기때문에 다양한 UI가 필요하고 상호작용을 하기위해 DOM 관리와 상태 변화 관리 등 개발자가 신경쓸 일이 많아진다. 
`React`를 사용하면 사용자와 상호작용할 수 있는 UI를 쉽게 만들 수 있다.

그렇다면 `React`의 특징을 살펴보자.

- **Component 기반**

`React`는 **컴포넌트 기반**라이브러리이다. `컴포넌트`는 UI를 구성하는 개별적인 뷰 단위로서, UI를 레고라고 한다면, `컴포넌트`는 블록역할을 하게 된다. 이러한 `컴포넌트`를 조립해 UI를 만들게 된다.

즉, 기존의 웹 페이지를 작성할 때 처럼 하나의 `HTML` 코드를 집어넣는 것이 아닌, 여러 부분을 분할하여 조립해 `View`를 만든다.

이러한 특징은 하나의 `컴포넌트`를 여러 부분에서 사용할 수 있게 하여 **코드의 재사용성과 유지보수성을 증가시켜 준다.**

쉽게 얘기하자면,

`컴포넌트` 기반이 아닌 방식으로 `View`를 만들 때 코드의 일부를 수정해야 한다면 다른 요소들에게 영향을 미칠 수가 있다.

하지만 `컴포넌트` 기반으로 코드를 짰다면 그 부분의 파일만 수정하면 되기때문에 유지보수가 쉽다. 이러한 `컴포넌트` 기반은 `React`의 가장 큰 장점이다.

``` html
<html>
  <head>
    <title>블로그</title>
  </head>
  <body>
    <header>
       <!-- 헤더 내용 -->
    </header>
    <div class="post-list">
       <!-- 콘텐츠 리스트 -->
    </div>
    <footer>
      <!-- 푸터 내용 -->
    </footer>
  </body>
</html>
```
위와 같은 어플리케이션이 있다고 하자. 이를 `React`로 만들게 되면 다음과 같다.
``` jsx
import React, { Component } from "react";
import Header from "./component/Header";
import Footer from "./component/Footer";
import PostList from "./component/PostList";

class App extends Component {
  render() {
    return(
      <div>
        <Header />
        <PostList />
        <Footer />
      </div>
    )
  }
}

export default App;
```
`Header`나 `Footer`, `PostList`를 컴포넌트로 만들어 이를 조립하여 화면을 구성하는 방식이다.

만약에 `Header`를 수정해야할 경우에는 `Header`만을 건드리면 되기 때문에 유지보수가 쉽다.
또한, 다른 프로젝트에서 다시 컴포넌트를 다시 쓸 수 있기때문에 재사용성이 뛰어나다.

- **JSX**

`JSX`는 자바스크립트 안에서 `HTML` 문법을 사용해서 `View`를 구성할 수 있게 도와주는 자바스크립트 문법이다. 
`react`에서 `element`를 제공해준다. 

```jsx
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}
```
위에 코드를 보면, `<div>`와 같이 HTML 태그가 보이는 것을 확인할 수 있다. 이것이 `JSX`이다.

`HTML` 문법과 유사한 `JSX`를 통해 `컴포넌트`를 생성할 수 있게 된다.

- **Virtual Dom**

유저의 인터랙션에 의해 상태 변화가 일어나면 [브라우저 작동 원리](https://github.com/im-d-team/Dev-Docs/blob/master/Browser/웹%20브라우저의%20작동%20원리.md)에 의해 렌더링 과정을 반복하게 된다. 

`Virtual Dom`은 이러한 과정에 의해 발생하는 비효율성을 최소화하기 위해 탄생하게 되었다.

사실 `Virtual Dom`은 기존 `DOM`의 한계를 탈피하기 위해 나온 대안이다. 
> DOM이란 Document Object Model로, 우리가 사용하는 HTML단위 하나하나(h1,li,html,body 등)를 객체로 생각한 모델이다.

`DOM`의 구조는 **트리 구조**로 되어 있다. 
만약 프로그래머가 `DOM`의 요소를 하나 수정하는 함수를 만들고 실행시킬 때, `렌더트리`를 재생성하고 `레이아웃`을 만들고 `페인팅`하는 과정이 다시 반복된다.

쉽게 말하면 `view`의 변화가 발생하여 10개의 노드를 수정해야 한다면, 10번의 레이아웃 재계산, 10번의 리랜더링이 필요하다는 것이다.

매번 `DOM`을 수정할 때 마다 **불필요한 연산이 매번 일어난다**는 것이다.

이러한 문제를 해결하기 위해서 `Virtual DOM`이 등장했다.
`Virtual DOM`은 변화가 발생하면 실제 `DOM`에 적용되기 전에 `Virtual DOM`에 적용을 시켜본다. 

`Vitual DOM`은 랜더링 과정이 필요 없기 때문에 연산 비용이 실제 `DOM`보다 적다.

`Virtual DOM`에서 이러한 연산이 끝나고 나면, 최종적인 변화를 실제 `DOM`에 전달해준다.

`Virtual DOM`은 바뀐 부분과 바뀌지 않은 부분을 자동으로 파악하여 필요한 DOM 트리만 업데이트할 수 있게 해준다.

따라서 필요한 트리만 변경이 되기 때문에 브라우저 렌더링 과정(HTML 파싱, 렌더 트리 구축, 렌더 트리 배치, 렌더 트리 그리기 과정)에 있어서
웹 브라우저의 동작에 적은 리소스가 요구된다.

이 [동영상](https://www.youtube.com/watch?v=muc2ZF0QIO4)을 보면 이해에 도움이 될 것이다.

## React 프로젝트 시작하기

- **create-react-app 설치**

`creact-react-app`은 페이스북에서 만든 `react` 웹 개발용 도구이다.
``` 
npm install -g create-rect-app
creat-react-app react-todo
```
위에 명령어를 터미널에 입력하여 리액트 앱을 설치하고 `react-todo`폴더를 생성한다. 

```tsx
cd react-todo
npm start
```
그 후 폴더 이동 후 프로젝트를 로컬에서 실행해볼 수 있다.

### creat-react-app 프로젝트의 구조
폴더는 아래와 같이 구성 되어있다.

<img width="678" alt="프로젝트 구조" src="https://user-images.githubusercontent.com/43868540/92316269-74fa2800-f02c-11ea-8ecf-e447b3c52bc0.png">

> [출처](https://eunvanz.github.io/react/2018/06/05/React-create-react-app으로-프로젝트-시작하기/)

위에 프로젝트의 구성 중 핵심적인 소스를 3가지이다.

- src/App.js
- src/index.js
- public/index.html

> public : 가상 DOM이 들어갈 빈 껍데기 html이다.

> src : 리액트 개발이 이루어지는 메인 폴더이다.

하나하나 뜯어보자.

- **App.js**
```jsx
import React, {Component} from 'react';   //react와 component를 불러오고 있다.
import './App.css'; //css파일을 import 구문으로 가져오고 있다. 

class App extends Component {
  render() {
    return (
      <div className="App">
       //화면에 출력될 내용
       <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
       </header>
      </div>
    );
  }
}

export default App; 
```
[컴포넌트를 만드는 방법](https://velog.io/@jiasong214/React-컴포넌트를-만드는-방법)에는 총 두 가지가 있는데 **클래스로 만드는 방법**과 **함수로 만드는 방법**이 있다.

우리는 클래스를 통하여 만드는 방법으로 컴포넌트를 만들겠다.

모든 `react` 컴포넌트들은 `react` 모듈의 `Component 클래스`를 상속받는다. 

`Component`는 추상 클래스이기 때문에 미리 정의해 둔 메소드들이 있고, 그 메소드들을 `override` 해서 `컴포넌트`들을 구현하는데, 그 중에서 화면을 그려주는 `render` 메소드는 필수적으로 정의해야 한다. 

`render` 메소드는 반드시 `jsx` 문법으로 작성해 **화면에 html 뷰를 생성**하는 역할을 한다.

마지막의 `export default App` 이 코드는 작성한 `컴포넌트`를 내보내는 코드이다.

`export`로 내보낸 `컴포넌트`는 다른 파일에서 `import`해서 사용할 수 있다.

`default`는 이 파일에서 기본적으로 `App` 컴포넌트 하나만 `export`한다는 의미다.

정리하자면

1. 리액트, 리액트 컴포넌트를 불러온다.
2. `App 클래스`를 만드는데, 그 클래스는 리액트 컴포넌트를 상속받는다.
3. 상속받은 리액트 컴포넌트 메소드 중, `render()` 메소드를 활용해서 html 코드를 작성해 `return` 시켜준다.
4. 이렇게 작성된 리액트 코드를 `export` 시켜준다.
5. 이 컴포넌트는 다른 파일에서 `import`해서 사용한다.

- **index.js**
```js
import React from 'react';              //jsx문법을 사용하기 위해서 react모듈을 import 해야한다. 모든 react 컴포넌트에 필수적인 코드이다.
import ReactDOM from 'react-dom';       //react-dom모듈은 react 앱을 최초 렌더링 하기위해 쓰인다.
import './index.css';                   //css파일을 import 구문으로 가져오고 있다.
import App from './App';                //App이라는 react 컴포넌트를 가져오는 코드이다. 

ReactDOM.render(<App />, document.getElementById('root'));    //컴포넌트를 렌더링하는 코드이다.
```
`root`라는 `id`를 가진 `DOM`를 찾아서 그 안에 `App 컴포넌트`를 렌더링시킨다.
`id`가 `root`인 `DOM`는 `index.html`에 있다. 즉, 화면에 보여질 템플릿 설정과 관련된 중요한 코드이다.

- **index.html**
``` html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <title>React App</title>
   </head>
   <body>
      <div id="root"></div>
   </body>
</html>
```
`id`가 `root`인 `DOM`을 생성한다. `index.js`에서 이 `DOM`을 찾아내 `App` 컴포넌트가 렌더링이 되어진다.

다음 시간에는 `React`에서 데이터를 관리하는 부분인 `Props`와 `State`에 관해서 알아보도록 하겠다.

----
#### Reference
- [Component 기반 구조](https://valuefactory.tistory.com/544)
- [React-part1](https://medium.com/wasd/기초부터-배우는-react-js-1531b18f7bb2)
- [React 파일 구조](https://velog.io/@hidaehyunlee/React-파일-구조-이해하기)
