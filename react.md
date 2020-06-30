# JSX
---
JSX: 자바스크립트의 확장 문법 -> 바벨 사용하여 일반 자바스크립트 형태의 코드로 변환

```react
function App() {
  return (
    <div>
      Hello <b>react</b>
    </div>
  );
}
```
는 다음과 같이 변경

```react
function App() {
return React.createElement("div", null, "Hello ", React.createElement("b", null, "react"));
}
```

> JSX의 장점
1. 보기 쉽고 편리하다.
2. html 태그 사용 가능 뿐만 아니라 컴포넌트 작성도 가능해 활용도 높음.

___
> ReactDOM.render

컴포넌트를 페이지에 렌더링하는 역할 및 react-dom 모듈 사용 가능하게 하는 역할.
이 코드는 컴포넌트를 페이지에 렌더링하는 역할을 하며, react-dom 모듈을 불러와 사용할 수 있습니다. 이 함수의 첫 번째 파라미터에는 페이지에 렌더링할 내용을 JSX 형태로 작성하고, 두 번째 파라미터에는 해당 JSX를 렌더링할 document 내부 요소를 설정합니다. 여기서는 id가 root인 요소 안에 렌더링을 하도록 설정했는데요. 이 요소는 public/index.html 파일을 열어 보면 있답니다.

> JSX 문법

컴포넌트에 여러 요소가 있다면 반드시 부모 요소 하나로 감싸야 한다. -> Virtual DOM에서 컴포넌트 변화를 감지해 낼 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다는 규칙이 있기 때문.

자바스크립트 표현하고자 할 때 -> { }로 감싸기.

조건에 따라 다른 내용을 렌더링해야 할 때는 JSX 밖에서 if문 사용 또는 조건부 연산자(삼항 연산자)를 { } 안에 사용.

<br>example</br>

```react
function App() {
  const name = '리액트';
  return (
    <div>
      {name === '리액트' ? (
        <h1>리액트입니다.</h1>
      ) : (
        <h2>리액트가 아닙니다.</h2>
      )}
    </div>
  );
}
```

&& 연산자를 이용시 조건부 렌더링 가능(0 제외)

undefined를 렌더링시 오류날 수 있으므로 ||(OR 연산자) 사용하거나 JSX 내부에서 렌더링하기.

리액트에서 DOM 요소에 스타일을 적용할 때는 문자열 형태로 넣는 것이 아니라 객체 형태로 넣어야 함.   
ex) - 문자를 없애고 카멜 표기법(camelCase)으로 작성해야 함.

class -> className

self-closing 태그 = <>, </>

주석 = {/* ... */}

# 컴포넌트
---

1. 데이터가 주어졌을 때 이에 맞추어 UI 생성. 
2. 라이프사이클 API를 이용하여 컴포넌트가 화면에서 나타날 때, 사라질 때, 변화가 일어날 때 주어진 작업들을 처리 가능. 
3. 임의 메서드를 만들어 특별한 기능 만들기 가능.

함수형 컴포넌트와 클래스형 컴포넌트

> 함수형 컴포넌트

1. 클래스형 컴포넌트보다 선언하기가 훨씬 편하다. 
2. 메모리 자원도 클래스형 컴포넌트보다 덜 사용.
3.  프로젝트를 완성하여 빌드한 후 배포할 때 결과물의 파일 크기가 더 작다.

```react
function App() {
  const name = '리액트';
  return <div className="react">{name}</div>;
}
```

> 클래스형 컴포넌트

1. state 기능 사용 가능, 라이프사이클 기능 사용 가능.( Hooks 이용하면 함수형 컴포넌트도 사용 가능)
2. 임의 메서드를 정의 가능.

```react
class App extends Component {
  render() {
    const name = 'react';
    return <div className="react">{name}</div>;
  }
}
```

일반 함수는 자신이 종속된 객체 = this, 
화살표 함수는 자신이 종속된 인스턴스 = this.

화살표 함수는 값을 연산하여 바로 반환해야 할 때 사용하면 가독성을 높일 수 있다.

> props

props = 컴포넌트 속성을 설정할 때 사용하는 요소. 

props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정 가능.

ex)
```react
const MyComponent = props => {
return <div>안녕하세요, 제 이름은 {props.name}입니다.</div>;
};

const App = () => {
  return <MyComponent name="React" />;
};
```

props 기본값 설정: defaultProps

<br>태그 사이의 내용을 보여 주는 children</br>

```react
const App = () => {
  return <MyComponent>리액트</MyComponent>;
};

const MyComponent = props => {
  return (
    <div>
      안녕하세요, 제 이름은 {props.name}입니다. <br />
      children 값은 {props.children}
      입니다.
    </div>
  );
};
```
<br>props 반복 피하기: 비구조화 할당</br>

```react
const MyComponent = props => {
  const { name, children } = props;
  return (
    <div>
      안녕하세요, 제 이름은 {name}입니다. <br />
      children 값은 {children}
      입니다.
    </div>
  );
};
```

컴포넌트의 필수 props를 지정하거나 props의 타입(type)을 지정할 때는 propTypes를 사용.

isRequired를 사용하면 필수 propTypes 설정 가능.

클래스형 컴포넌트에서 props를 사용할 때는 render 함수에서 this.props.

<br>클래스형 컴포넌트에서 defaultProps와 propTypes를 설정할 때 class 내부에서 지정하는 방법.</br>

```react
class MyComponent extends Component {
  static defaultProps = {
    name: '기본 이름'
  };
  static propTypes = {
    name: PropTypes.string,
    favoriteNumber: PropTypes.number.isRequired
  };
  render() {
    const { name, favoriteNumber, children } = this.props; // 비구조화 할당
    return (...);
  }
}
```

> state

state: 컴포넌트 내부에서 바뀔 수 있는 값.

1. 클래스형 컴포넌트가 지니고 있는 state.
2. 함수형 컴포넌트에서 useState라는 함수를 통해 사용하는 state.

```react
constructor(props) {
  super(props);
  // state의 초깃값 설정하기
  this.state = {
      number: 0
    };
  }
  ```
