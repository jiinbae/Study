# JSX

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

<strong>example</strong>

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
컴포넌트 자신은 해당 props를 읽기 전용으로만 사용 가능하므로 props를 바꾸려면 부모 컴포넌트에서 변경해야 함.

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

<strong>태그 사이의 내용을 보여 주는 children</strong>

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
<strong>props 반복 피하기: 비구조화 할당</strong>

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

<strong>클래스형 컴포넌트에서 defaultProps와 propTypes를 설정할 때 class 내부에서 지정하는 방법.</strong>

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
  컴포넌트의 state는 객체 형식.

```react
  render() {
  const { number } = this.state; // state를 조회할 때는 this.state로 조회합니다.
  return (
      <div>
        <h1>{number}</h1>
        <button
        // onClick을 통해 버튼이 클릭되었을 때 호출할 함수를 지정합니다.
        onClick={() => {
          // this.setState를 사용하여 state에 새로운 값을 넣을 수 있습니다.
          this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
```

state 객체는 여러 값 가지기 가능.

<strong>construct 메서드 선언 없이 state 초깃값 설정</strong>
```react
class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0
  };
  render() {
    const { number, fixedNumber } = this.state; // state를 조회할 때는 this.state로 조회합니다.
    return (...);
  }
}
```

this.setState가 끝난 후 특정 작업 실행하려면 setState의 두 번째 파라미터로 콜백 함수 호출.

useState 사용하여 함수형 컴포넌트에서도 state 사용 가능.

<strong>배열 비구조화 할당</strong>

```react
const array = [1, 2];
const [one, two] = array;
```

<strong>useState 사용하는 법</strong>

```react
import React, { useState } from 'react';
 
const Say = () => {
  const [message, setMessage] = useState('');
  const onClickEnter = () => setMessage('안녕하세요!');
  const onClickLeave = () => setMessage('안녕히 가세요!');
 
  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      <h1>{message}</h1>
    </div>
  );
};
```

# 이벤트 핸들링

> react의 이벤트 시스템

<strong>주의사항</strong>
1. 이벤트 이름은 카멜 표기법으로 작성.
2. 함수 형태의 값 전달.
3. DOM 요소에만 이벤트 설정 가능.<br>
컴포넌트 자체적으로 이벤트 설정은 불가능하지만, 전달받은 props를 컴포넌트 내부의 DOM 이벤트로 설정 가능.

```react
<div onClick={this.props.onClick}>
```

비동기적으로 이벤트 객체를 참조할 일이 있다면 e.persist() 함수를 호출

<strong>state에 input값 넣기</strong>

```react
class EventPractice extends Component {

    state = {
        message: ''
      }

  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input
          type="text"
          name="message"
          placeholder="아무거나 입력해 보세요"
          value={this.state.message}
          onChange={
            (e) => {
              this.setState({
                message: e.target.value
              })
            }
          }
        />
        <button onClick={
          () => {
            alert(this.state.message);
            this.setState({
              message: ''
            });
          }
        }>확인</button>
      </div>
    );
  }
}
```

this를 컴포넌트 자신을 가르키게 하려면 메서드와 this를 binding하는 작업이 필요.

<strong>ex)</strong>

```react
constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleClick = this.handleClick.bind(this);
  }
```

바벨의 transform-class-properties 문법을 사용하여 화살표 함수 형태로 메서드를 정의하면 생성자 메서드에 따로 정의할 필요 X.

<strong>ex)</strong>

```react
handleChange = (e) => {
    this.setState({
      message: e.target.value
    });
  }
 
  handleClick = () => {
    alert(this.state.message);
    this.setState({
      message: ''
    });
  }
```

객체 안에서 key를 [ ]로 감싸면 그 안에 넣은 레퍼런스가 가리키는 실제 값이 key 값으로 사용.
```react
handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
};
```

<strong>여러 input 다루기</strong>
```react
const EventPractice = () => {
    const [userInput, setUserInput] = useState({id:'jiin', age:'23'});
    const onChangeUserInput = e => {
        const newObject = { ...userInput }
        newObject[e.target.name] = e.target.value;
        setUserInput(newObject);
        console.log(newObject);
    }
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input
          type="text"
          name="id"
          value={userInput.username}
          onChange={onChangeUserInput}
        />
        <input
          type="text"
          name="age"
          value={userInput.age}
          onChange={onChangeUserInput}
        />
      </div>
    );
  };
```
# ref: DOM에 이름 달기

```react
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root') // id가 root인 요소에 리액트 컴포넌트를 렌더링하라는 코드
);
```
> ref

: 리액트 프로젝트 내부에서 DOM에 이름을 다는 방법.

DOM을 꼭 직접적으로 건드려야 할 때 사용.<br>
1. 특정 input에 포커스 주기
2. 스크롤 박스 조작하기
3. Canvas 요소에 그림 그리기

> ref 만드는 방법

<strong>1. 콜백 함수 이용</strong>

```react
<input ref={(ref) => {this.input=ref}} /> //this.input은 input 요소의 DOM을 가리킨다.
```

ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달 =><br>이 콜백 함수는 ref 값을 파라미터로 전달받고 =><br>함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정.

<strong>2. createRef 함수 사용</strong>

ex)
```react
class RefSample extends Component {
  input = React.createRef(); // 컴포넌트 내부에서 멤버 변수로 React.createRef()를 담아주기.
 
  handleFocus = () => {
    this.input.current.focus(); // ref를 설정해 준 DOM에 접근할 때
  }

  render() {
    return (
      <div>
        <input ref={this.input} />
      </div>
    );
  }
}
```

> 컴포넌트에 ref 달기

```react
<MyComponent
  ref={(ref) => {this.myComponent=ref}}
/>
```


