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
1. 포커스, 텍스트 선택 영역, 혹은 미디어의 재생을 관리할 때.
2. 애니메이션을 직접적으로 실행시킬 때.
3. 서드 파티 DOM 라이브러리를 React와 같이 사용할 때.

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

# 컴포넌트 반복

> map 함수

: 파라미터로 전달된 함수를 사용 =><br>
배열 내 각 요소를 원하는 규칙에 따라 변환 =><br>
그 결과로 새로운 배열 생성.

arr.map(callback, [thisArg])

• callback: 새로운 배열의 요소를 생성하는 함수.
   - currentValue: 현재 처리하고 있는 요소
   - index: 현재 처리하고 있는 요소의 index 값
   - array: 현재 처리하고 있는 원본 배열<br>

• thisArg(선택 항목): callback 함수 내부에서 사용할 this 레퍼런스

> key

: 컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있었는지 알아내려고 사용.
(key값은 언제나 유일해야 한다.)

고유한 값이 없을 때 index 값을 key로 사용. (하지만 리렌더링 비효율적.)

<strong>초기 상태 설정</strong>

1. 데이터 배열
2. 텍스트를 입력할 수 있는 input의 상태
3. 새로운 항목을 추가할 때 사용할 고유 id를 위한 상태

불변성 유지: 리액트에서 상태를 업데이트할 때는 기존 상태를 그대로 두면서 새로운 값을 상태로 설정해야 함.

배열의 특정 항목 추가 : concat 함수, 배열의 특정 항목 삭제: filter 함수.

# 라이프사이클 메서드 (수명 주기)

컴포넌트의 수명은 페이지에 렌더링되기 전인 준비과정에서 시작, 페이지에서 사라질 때 종료.

라이프사이클 메서드 (9가지)
1. Will 접두사: 어떤 작업 작동 전 실행 메서드.
2. Did 접두사: 어떤 작업 작동 후 실행 메서드.

- 마운트: 페이지에 컴포넌트가 나타남.
- 업데이트: 컴포넌트 정보를 업데이트.
- 언마운트: 페이지에서 컴포넌트가 사라짐.

> 마운트

```
컴포넌트 만들기 =>
constructor: 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드 =>
getDerivedStateFromProps: props에 있는 값을 state에 넣을 때 사용하는 메서드 =>
render: 우리가 준비한 UI를 렌더링하는 메서드 =>
componentDidMount: 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드
```

> 업데이트

1. props 바뀔 때
2. state 바뀔 때
3. 부모 컴퍼넌트 리렌더링될 때
4. this.forceUpdate로 강제로 렌더링을 트리거할 때

```
업데이트 발생 요인 =>
getDerivedStateFromProps: props의 변화에 따라 state 값에도 변화를 주고 싶을 때 사용 =>
shouldComponentUpdate: 컴포넌트가 리렌더링을 해야 할지 말아야 할지를 결정하는 메서드. true 반환 시 render 호출, false 반환 시 여기서 작업 취소 (this.forceUpdate() 호출 시 생략 후 render 함수 호출) =>
render: 컴포넌트 리렌더링 =>
getSnapshotBeforeUpdate: 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드 =>
componentDidUpdate: 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드
```

> 언마운트

```
언마운트 하기 => componentWillUnmount
```

componentWillUnmount: 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드.

> 라이프사이클 메서드

<strong>render() 함수</strong>

```
render() { ... }
```

컴포넌트 모양새 정의.<br>
라이프사이클 메서드 중 유일한 필수 메서드.<br>
이 메서드 안에서 this.props와 this.state에 접근할 수 있으며, 리액트 요소를 반환.(div 태그나 따로 선언한 컴포넌트)<br>
이벤트 설정이 아닌 곳에서 setState 사용 불가, 브라우저의 DOM에 접근도 안됨. (처리하고자 할 때는 componentDidMount에서)

<strong>constructor() 메서드</strong>

```
constructor(props) { ... }
```

컴포넌트의 생성자 메서드.<br>
초기 state 설정 가능.

<strong>getDerivedStateFromProps 메서드</strong>

```react
static getDerivedStateFromProps(nextProps, prevState) {
    if(nextProps.value != = prevState.value) { // 조건에 따라 특정 값 동기화
      return { value: nextProps.value };
    }
    return null; // state를 변경할 필요가 없다면 null을 반환
}
```

 props로 받아 온 값을 state에 동기화시키는 용도.<br>
 컴포넌트가 마운트될 때와 업데이트될 때 호출.

 <strong>componentDidMount 메서드</strong>

 ```
 componentDidMount() { ... }
 ```

컴포넌트를 만들고, 첫 렌더링을 다 마친 후 실행.<br>
다른 자바스크립트 라이브러리 또는 프레임워크의 함수를 호출하거나 이벤트 등록, setTimeout, setInterval, 네트워크 요청 같은 비동기 작업을 처리.

<strong>shouldComponentUpdate 메서드</strong>

 ```
shouldComponentUpdate(nextProps, nextState) { ... }
 ```

 props 또는 state를 변경했을 때, 리렌더링을 시작할지 여부를 지정하는 메서드.<br>
 반드시 true 값 또는 false 값을 반환해야 하고, false 값 반환 시 업데이트 중지. (기본적으로 true값 반환)<br>
이 메서드 안에서 현재 props와 state는 this.props와 this.state로 접근하고, 새로 설정될 props 또는 state는 nextProps와 nextState로 접근.

<strong>getSnapshotBeforeUpdate 메서드</strong>

 ```react
getSnapshotBeforeUpdate(prevProps, prevState) {
    if(prevState.array != = this.state.array) {
    const { scrollTop, scrollHeight } = this.list
      return { scrollTop, scrollHeight };
    }
}
 ```

render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출.<br>
이 메서드에서 반환하는 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값.<br>
업데이트하기 직전의 값을 참고할 일이 있을 때 활용.

<strong>componentDidUpdate 메서드</strong>

 ```
 componentDidUpdate(prevProps, prevState, snapshot) { ... }
 ```

 리렌더링 완료 후 실행.<br>
 DOM 관련 처리 가능.<br>
 prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근 가능.<br>
 getSnapshotBeforeUpdate에서 반환한 값이 있다면 여기서 snapshot 값을 전달받음.

 <strong>componentWillUnmount 메서드</strong>

 ```
 componentWillUnmount() { ... }
 ```

컴포넌트를 DOM에서 제거할 때 실행. (componentDidMount에서 등록한 이벤트, 타이머, 직접 생성한 DOM)

<strong>componentDidCatch 메서드</strong>

 ```react
 componentDidCatch(error, info) {
  this.setState({
    error: true
  });
  console.log({ error, info });
}
 ```

컴포넌트 렌더링 도중에 에러가 발생했을 때 오류 UI 보여줌.<br>
error: 파라미터에 어떤 에러 발생했는지.<br>
info: 어디에 있는 코드에서 오류가 발생했는지.<br>
서버 API를 호출하여 따로 수집 가능.<br>
컴포넌트 자신에게 발생하는 에러를 잡아낼 수 X, 자신의 this.props.children으로 전달되는 컴포넌트에서 발생하는 에러만 잡아낼 수 O.

