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

<strong>example</strong>

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

<strong>example</strong>

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

# Hooks

> useState

이 함수의 파라미터에는 상태의 기본 값.<br>
함수 호출 시 배열 반환 => 첫 번째 원소: 상태 값, 두 번째 원소: 상태 설정 함수.<br>
파라미터 넣어서 호출 시 전달 받은 파라미터로 값 변하고 컴포넌트 리렌더링.

> useEffect

리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook.<br>
클래스형 컴포넌트의 componentDidMount + componentDidUpdate 형태.

<strong>마운트될 때만 실행하고 싶을 때</strong>

useEffect에서 설정한 함수를 컴포넌트가 화면에 맨 처음 렌더링될 때만 실행하고, 업데이트될 때는 X => 함수의 두 번째 파라미터로 비어 있는 배열 추가.

```react
useEffect(() => {
    console.log('마운트될 때만 실행됩니다.');
  }, []);
  ```

<strong>특정 값이 업데이트될 때만 실행하고 싶을 때</strong>

useEffect의 두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값 추가.

```react
useEffect(() => {
  console.log(name);
}, [name]);
```
<strong>컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면 => 뒷정리(cleanup) 함수를 반환.</strong>

```react
useEffect(() => {
  console.log('effect');
  console.log(name);
  return () => {
    console.log('cleanup');
    console.log(name);
  };
});
```

언마운트될 때만 뒷정리 함수를 호출.

```react
useEffect(() => {
  console.log('effect');
  console.log(name);
  return () => {
    console.log('cleanup');
    console.log(name);
  };
}, []);
```

> useReducer

: useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트해 주고 싶을 때 사용하는 Hook.

현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션 값을 전달받아 새로운 상태를 반환하는 함수.<br>
리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜 주어야 함.

```react
function reducer(state, action) {
return { ... }; // 불변성을 지키면서 업데이트한 새로운 상태 반환.
}
```

액션 값
```react
{
  type: 'INCREMENT',
  // 다른 값들은 필요 시 추가.
}
```

useReducer의 첫 번째 파라미터: 리듀서 함수, 두 번째 파라미터: 해당 리듀서의 기본값.

state는 현재 가리키고 있는 상태고, dispatch는 액션을 발생시키는 함수.

컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 것이 장점.

> useMemo

useMemo Hook을 사용하면 함수형 컴포넌트 내부에서 발생하는 연산을 최적화.<br> 렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식.

> useCallback

렌더링 성능을 최적화해야 하는 상황에서 사용.<br>
이벤트 핸들러 함수를 필요할 때만 생성.

 첫 번째 파라미터: 생성하고 싶은 함수, 두 번째 파라미터에는 배열.<br>
 비어있는 배열 => 컴포넌트가 렌더링될 때 단 한 번만 함수가 생성.

<strong>example</strong>

```react
useCallback(() => {
  console.log('hello world!');
}, []) // 배열 안에 내용 추가시 인풋 내용이 바뀌거나 새로운 항목이 추가될 때마다 함수가 생성.
 
useMemo(() => {
  const fn = () => {
    console.log('hello world!');
  };
  return fn;
}, [])
```

숫자, 문자열, 객체처럼 일반 값을 재사용하려면 useMemo를 사용하고, 함수를 재사용하려면 useCallback을 사용.

> useRef

useRef Hook은 함수형 컴포넌트에서 ref를 쉽게 사용 가능하게 만들어준다.<br>
useRef를 사용하여 ref 설정 시 useRef를 통해 만든 객체 안의 current 값이 실제 엘리먼트를 가리킨다.

컴포넌트 로컬 변수를 사용할 때도 이용 가능.<br>
로컬 변수: 렌더링과 상관없이 바뀔 수 있는 값.

<strong>example</strong>

```react
// 클래스형 컴포넌트
import React, { Component } from 'react';
 
class MyComponent extends Component {
  id = 1
  setId = (n) => {
    this.id = n;
  }
  printId = () => {
    console.log(this.id);
  }
  render() {
    return (
      <div>
        MyComponent
      </div>
    );
  }
}
 
export default MyComponent;

// 함수형 컴포넌트
import React, { useRef } from 'react';
 
const RefSample = () => {
  const id = useRef(1);
  const setId = (n) => {
    id.current = n;
  }
  const printId = () => {
    console.log(id.current);
  }
  return (
    <div>
      refsample
    </div>
  );
};
 
export default RefSample;
```

ref 안의 값이 바뀌어도 컴포넌트가 렌더링되지 않으므로 렌더링과 관련되지 않은 값을 관리할 때만 사용.

# 컴포넌트 스타일링

• 일반 CSS: 컴포넌트를 스타일링하는 가장 기본적인 방식.<br>
• Sass: 자주 사용되는 CSS 전처리기(pre-processor) 중 하나로 확장된 CSS 문법을 사용하여 CSS 코드 더욱 쉽게 작성 가능.<br>
• CSS Module: 스타일을 작성할 때 CSS 클래스가 다른 CSS 클래스의 이름과 절대 충돌하지 않도록 파일마다 고유한 이름을 자동으로 생성해 주는 옵션.<br>
• styled-components: 스타일을 자바스크립트 파일에 내장시키는 방식으로 스타일을 작성함과 동시에 해당 스타일이 적용된 컴포넌트 생성.<br>

> CSS를 작성할 때 중요한 점

CSS 클래스를 중복되지 않게 만드는 것.
1. 이름을 지을 때 특별한 규칙을 사용하여 짓는 것.
2.  CSS Selector를 활용하는 것.

컴포넌트 이름-클래스 형태.<br>
BEM 네이밍: CSS 방법론 중 하나로, 이름을 지을 때 일종의 규칙을 준수하여 해당 클래스가 어디에서 어떤 용도로 사용되는지 명확하게 작성하는 방식.

> CSS Selector

CSS 클래스가 특정 클래스 내부에 있는 경우에만 스타일을 적용 가능.<br>
컴포넌트의 최상위 html 요소에는 컴포넌트의 이름으로 클래스 이름을 짓고, 그 내부에서는 소문자를 입력하거나, header 같은 태그를 사용. (불필요한 경우 생략)

> Sass(Syntactically Awesome Style Sheets): CSS 전처리기.

1. 복잡한 작업을 쉽게 할 수 있도록 만들어준다.
2. 스타일 코드의 재활용성을 높여준다.
3. 코드의 가독성을 높여서 유지 보수를 더욱 쉽게 해준다.

> CSS Module

: CSS를 불러와서 사용할 때 클래스 이름을 고유한 값, 즉 [파일 이름]_[클래스 이름]__[해시값] 형태로 자동으로 만들어서 컴포넌트 스타일 클래스 이름이 중첩되는 현상을 방지해 주는 기술.

해당 클래스는 우리가 방금 만든 스타일을 직접 불러온 컴포넌트 내부에서만 작동.<br>
웹 페이지에서 전역적으로 사용되는 경우라면 :global을 앞에 입력.

고유한 클래스 이름을 사용하려면 클래스를 적용하고 싶은 JSX 엘리먼트에 className= {styles.[클래스 이름]} 형태로 전달.

classnames: CSS 클래스를 조건부로 설정시 사용하는 라이브러리.

<strong>example</strong>

```react
import classNames from 'classnames';
 
classNames('one', 'two'); // = 'one two'
classNames('one', { two: true }); // = 'one two'
classNames('one', { two: false }); // = 'one'
classNames('one', ['two', 'three']); // = 'one two three'
 
const myClass = 'hello';
classNames('one', myClass, { myCondition: true }); // = 'one hello myCondition'
```

props 값에 따라 다른 스타일 제공 용이.

<strong>example</strong>
```react
const MyComponent = ({ highlighted, theme }) => (
  <div className={classNames('MyComponent', { highlighted }, theme)}>Hello</div> // 엘리먼트의 클래스에 highlighted 값이 true이면 highlighted 클래스가 적용, false이면 적용 X.
);
```

내장되어 있는 bind 함수를 사용 시 cx('클래스 이름', '클래스 이름2') 형태로 사용 가능.

> CSS-in-JS

: 자바스크립트 파일 안에 스타일을 선언하는 방식.

styled-components를 사용하면 자바스크립트 파일 하나에 스타일까지 작성할 수 있기 때문에 .css 또는 .scss 확장자를 가진 스타일 파일을 따로 만들지 않아도 됨.

styled-components와 일반 classNames를 사용하는 CSS/Sass를 비교했을 때, 가장 큰 장점은 props 값으로 전달해 주는 값을 쉽게 스타일에 적용 가능하다는 것.

Tagged 템플릿 리터럴 : `을 사용하여 만든 문자열에 스타일 정보를 줌.<br>
이러한 속성을 사용하여 styled-components로 만든 컴포넌트의 props를 스타일 쪽에서 쉽게 조회 할 수 있게 만들어 줌.

스타일링된 엘리먼트 만들기.

<strong>example</strong>

```react
import styled from 'styled-components';
 
const MyComponent = styled.div`
  font-size: 2rem;
`;
```

사용해야 할 태그명이 유동적이거나 특정 컴포넌트 자체에 스타일링해 주고 싶은 경우.

<strong>example</strong>

```react
// 태그의 타입을 styled 함수의 인자로 전달
const MyInput = styled('input')`
  background: gray;
`
// 아예 컴포넌트 형식의 값을 넣어 줌
const StyledLink = styled(Link)`
  color: blue;
`
```

컴포넌트를 styled의 파라미터에 넣는 경우에는 해당 컴포넌트에 className props를 최상위 DOM의 className 값으로 설정하는 작업이 내부적으로 되어 있어야 함.

<strong>example</strong>

```react
const Sample = ({ className }) => {
  return <div className={className}>Sample</div>;
};
 
const StyledSample = styled(Sample)`
  font-size: 2rem;
`;
```

styled-components를 사용하면 스타일 쪽에서 컴포넌트에게 전달된 props 값을 참조 가능.

<strong>example</strong>

```react
const Box = styled.div`
  /* props로 넣어 준 값을 직접 전달해 줄 수 있습니다. */
  background: ${props => props.color || 'blue'};
  padding: 1rem;
  display: flex;
`;
```

props에 따른 조건부 스타일링

<strong>example</strong>

```react
/* 다음 코드는 inverted 값이 true일 때 특정 스타일을 부여해 줍니다. */
  ${props =>
    props.inverted &&
    css`
      background: none;
      border: 2px solid white;
      color: white;
      &:hover {
        background: white;
        color: black;
      }
    `};
```

styled-components 매뉴얼에서 제공하는 유틸 함수 => size 객체에 따라 자동으로 media 쿼리 함수를 만들어준다.

<strong>example</strong>

```react
const media = Object.keys(sizes).reduce((acc, label) => {
acc[label] = (...args) => css`
  @media (max-width: ${sizes[label] / 16}em) {
    ${css(...args)};
    }
`;
 
return acc;
}, {});
```

# TODOList Project

주요 컴포넌트들
1. TodoTemplate: 화면을 가운데에 정렬, 앱 타이틀(일정 관리)을 보여줌. children으로 내부 JSX를 props로 받아 와서 렌더링.
2. TodoInsert: 새로운 항목을 입력, 추가할 수 있는 컴포넌트. state를 통해 인풋의 상태를 관리.
3. TodoListItem: 각 할 일 항목에 대한 정보를 보여 주는 컴포넌트. todo 객체를 props로 받아 와서 상태에 따라 다른 스타일의 UI를 보여줌.
4. TodoList: todos 배열을 props로 받아 온 후, 이를 배열 내장 함수 map을 사용해서 여러 개의 TodoListItem 컴포넌트로 변환하여 보여줌.


# 컴포넌트 성능 최적화

컴포넌트는 다음 같은 상황에서 리렌더링 발생.
1. 자신이 전달받은 props가 변경될 때.
2. 자신의 state가 바뀔 때.
3. 부모 컴포넌트가 리렌더링될 때.
4. forceUpdate 함수가 실행될 때.

React.memo를 사용하여 컴포넌트 성능 최적화.

todos 배열이 바뀔 때마다 함수가 새로 만들어지는 상황을 방지하는 방법.
1. useState의 함수형 업데이트 기능을 사용하는 것.
2. useReducer를 사용하는 것.

함수형 업데이트: setTodos를 사용할 때 새로운 상태를 파라미터로 넣는 대신, 상태 업데이트를 어떻게 할지 정의해 주는 업데이트 함수를 넣는 것.

<strong>프로덕션 모드로 구동하는 법</strong>

$ yarn build<br>
$ yarn global add serve<br>
$ serve -s build

> 불변성

업데이트가 필요한 곳에서는 아예 새로운 배열 혹은 새로운 객체를 만들기 때문에, React.memo를 사용했을 때 props가 바뀌었는지 혹은 바뀌지 않았는지를 알아내서 리렌더링 성능을 최적화.

불변성을 지킨다: 기존의 값을 직접 수정하지 않으면서 새로운 값을 만들어 내는 것.

전개 연산자(... 문법)를 사용하여 객체나 배열 내부의 값을 복사 => 얕은 복사.

객체 안 객체일 경우<br>
<strong>example</strong>

```react
const nextComplexObject = {
  ...complexObject,
  objectInside: {
    ...complexObject.objectInside,
    enabled: false
  }
};
console.log(complexObject === nextComplexObject); // false
console.log(complexObject.objectInside === nextComplexObject.objectInside); // false
```

리스트 관련 컴포넌트를 작성할 때는 리스트 아이템과 리스트, 이 두 가지 컴포넌트를 최적화 해주어야 한다.

> react-virtualized를 사용한 렌더링 최적화

리스트 컴포넌트에서 스크롤되기 전에 보이지 않는 컴포넌트는 렌더링하지 않고 크기만 차지하게끔 할 수 있습니다. 그리고 만약 스크롤되면 해당 스크롤 위치에서 보여 주어야 할 컴포넌트를 자연스럽게 렌더링시키죠. 이 라이브러리를 사용하면 낭비되는 자원을 아주 쉽게 아낄 수 있습니다.

# immer

```react
import produce from 'immer';
const nextState = produce(originalState, draft => {
  // 바꾸고 싶은 값 바꾸기
  draft.somewhere.deep.inside = 5;
})
```

조금 더 복잡한 데이터를 업데이트할 경우
```react
produce 함수<br> 첫 번째 파라미터: 수정하고 싶은 상태, 두 번째 파라미터: 상태를 어떻게 업데이트할지 정의하는 함수.

두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해 주면서 새로운 상태를 생성.

import produce from 'immer';
 
const originalState = [
  {
    id: 1,
    todo: '전개 연산자와 배열 내장 함수로 불변성 유지하기',
    checked: true,
  },
  {
    id: 2,
    todo: 'immer로 불변성 유지하기',
    checked: false,
  }
];
 
const nextState = produce(originalState, draft => {
  // id가 2인 항목의 checked 값을 true로 설정
  const todo = draft.find(t => t.id === 2); // id로 항목 찾기
  todo.checked = true;
    // 혹은 draft[1].checked = true;
 
  // 배열에 새로운 데이터 추가
  draft.push({
    id: 3,
    todo: '일정 관리 앱에 immmer 적용하기',
    checked: false,
  });
 
  // id = 1인 항목을 제거하기
  draft.splice(draft.findIndex(t => t.id === 1), 1);
});
```
immer에서 제공하는 produce 함수 호출 시, 첫 번째 파라미터가 함수 형태라면 업데이트 함수를 반환.

<strong>example</strong>
```react
const update = (draft => {
  draft.value = 2;
});
const originalState = {
  value: 1,
  foo: 'bar',
};
const nextState = update(originalState);
console.log(nextState); // { value: 2, foo: 'bar' }
```

# 리액트 라우터로 SPA 개발하기

SPA: Single Page Application

애플리케이션을 브라우저에 불러와서 실행 -> 사용자와의 인터랙션 발생 -> 해당 부분만 자바스크립트 사용하여 업데이트 (새로운 데이터 필요 시 서버 API 호출 -> 필요한 데이터만 사용)

SPA 단점
자바스크립트 파일 크기 커짐, 페이지 비어 있는 시간동안 흰 페이지 나타날 수도 O -> 서버 사이드 렌더링으로 해결 가능.

BrowserRouter: 웹 애플리케이션에 HTMl5의 history API를 사용하여 새로고침없이 주소 변경, 현 주소 관련 정보를 props로 쉽게 조회하거나 사용 가능하게 해주는 것.

Router 컴포넌트 사용하여 사용자의 현재 경로에 따라 다른 컴포넌트.

```react
<Route path="주소규칙" component={보여 줄 컴포넌트} />
```

> link

`<a>` 와 같이 다른 주소 이동 역할이지만 페이지 전환 방지하여 렌더링된 컴포넌트들도 그대로.

```react
<Link to="주소">내용</Link>
```

> URL 파라미터와 쿼리

페이지 주소 정의 시 유동적인 값을 전달할 때 사용.

파라미터: 특정 아이디, 이름<br>
쿼리: 키워드, 옵션 (location 객체에 들어있는 search 값에서 조회 가능)

쿼리 location의 형태<br>
<strong>example</strong>

```react
{
"pathname": "/about",
"search": "?detail=true",
"hash": ""
}
```
쿼리 문자열을 객체로 파싱하는 과정에서 결과 값은 언제나 문자열.

> 서브 라우트

라우트 내부에 또 라우트 정의.

첫 번째 Route 컴포넌트에는 component 대신 render라는 props.
컴포넌트 자체를 전달하는 것이 아니라, 보여 주고 싶은 JSX도 가능.
1. 따로 컴포넌트를 만들기 애매한 상황에 사용,
2. 컴포넌트에 props를 별도로 넣어 주고 싶을 때도 사용 가능.

> 리액트 라우터 부가 기능

- history: 컴포넌트 내에 구현하는 메서드에서 라우터 API 호출 가능.
- withRouter: HoC, 라우트로 사용된 컴포넌트가 아니어도 match, location, history 객체 접근 가능.<br>
withRouter를 사용하면 현재 자신을 보여 주고 있는 라우트 컴포넌트를 기준으로 match가 전달.
- Switch: 여러 Route를 감싸서 그중 일치하는 단 하나의 라우트만을 렌더링. 모든 규칙과 일치하지 않을 때 보여 줄 Not Found 페이지 구현 가능.
- NavLink: 현재 경로와 Link에서 사용하는 경로가 일치하는 경우 특정 스타일 혹은 CSS 클래스를 적용할 수 있는 컴포넌트.<br> 
링크가 활성화되었을 때: activeStyle 값,<br>
CSS 클래스를 적용할 때: activeClassName 값을 props.

# 외부 API 연동하여 뉴스 뷰어

웹 애플리케이션에서 서버 쪽 데이터 필요 -> Ajax 기법 사용 -> 서버 API 호출 -> 데이터 수신.

동기적으로 처리시 데이터 수신 때까지 아무것도 못 하는데, 비동기적 처리시 동시에 여러 가지 요청 처리 가능 & 다른 함수도 호출 가능.

> Promise

: 콜백 반복 없게 도와주는 기능.

```react
function increase(number) {
const promise = new Promise((resolve, reject) => {
  // resolve는 성공, reject는 실패
  setTimeout(() => {
    const result = number + 10;
    if (result > 50) {
      // 50보다 높으면 에러 발생
      const e = new Error('NumberTooBig');
      return reject(e);
    }
    resolve(result); // number 값에 +10 후 성공 처리
  }, 1000);
});
return promise;
}

increase(0)
.then(number => {
  // Promise에서 resolve된 값은 .then을 통해 받아 올 수 있음
  console.log(number);
  return increase(number); // Promise를 리턴하면
})
.then(number => {
  // 또 .then으로 처리 가능
  console.log(number);
  return increase(number);
})
.catch(e => {
  // 도중에 에러가 발생한다면 .catch를 통해 알 수 있음
  console.log(e);
});
```

> async/await

함수 앞 async 사용, 함수 내부 promise 앞 await 사용 => Promise가 끝날 때까지 기다리고, 결과 값을 특정 변수에 넣을 수 O.
(try, catch로 에러 처리)

> axios로 API 호출 => 데이터 받기

axios: 자바스크립트 HTTP 클라이언트. HTTP 요청을 Promise 기반으로 처리.<br>
axios.get함수: 파라미터로 전달된 주소에 GET 요청, then으로 결과 확인 가능.(비동기적)

뉴스 데이터가 지니고 있는 정보
- title: 제목
- description: 내용
- url: 링크
- urlToImage: 뉴스 이미지

useEffect 사용하여 컴포넌트가 처음 렌더링되는 시점에 API 요청 => 컴포넌트가 화면에 보이는 시점에 API 요청. (useEffect에서 반환해야 하는 값은 뒷정리 함수이기 때문에 async 붙이면 X -> 사용하고 싶다면 async 붙은 다른 함수 만들어서 사용해야 함.)

# Context API

기존에는 최상위 컴포넌트에서 여러 컴포넌트를 거쳐 props로 원하는 상태와 함수를 전달했지만, Context API를 사용하면 Context를 만들어 단 한 번에 원하는 값을 받아 와서 사용 가능.

> Render Props

컴포넌트 사이에 중괄호를 열어서 함수 넣는 방법.<br>
컴포넌트의 children이 있어야 할 자리에 일반 JSX 혹은 문자열이 아닌 함수 전달.

<strong>example</strong>

```react
import React from 'react';
 
const RenderPropsSample = ({ children }) => {
  return <div>결과: {children(5)}</div>;
};
 
export default RenderPropsSample;
```

```react
<RenderPropsSample>{value => 2 * value}</RenderPropsSample>;
```

RenderPropsSample에게 children props로 파라미터에 2를 곱해서 반환하는 함수를 전달하면 해당 컴포넌트에서는 이 함수에 5를 인자로 넣어서 10를 렌더링한다.

> 동적 context

Context value에는 상태 값이나 함수가 올 수 있다.

createContext의 기본값은 실제 Provider의 value에 넣는 객체 형태와 일치시켜주는 것이 권장됨.<br>
1. Context 코드를 볼 때 내부 값이 어떻게 구성되어 있는지 파악 용이.
2. 실수로 Provider를 사용하지 않았을 때 리액트 애플리케이션에서 에러 발생 X.

static contextType을 정의하면 클래스 메서드에서도 Context에 넣어 둔 함수를 호출할 수 있다. 하지만 한 클래스에서 하나의 Context밖에 사용하지 X.