## callback
---

> 콜백 함수

: 조건을 등록해 두고 그 조건을 만족했을 때 호출되는 함수.<br><br>

```javascript
function callback(cb){
    cb();
}

function add(x, y){
    let sum = x + y;
    callback( function() { // add 함수는 3과 5를 인자로 받아 더한 값을 sum에 할당하고, sum변수를 콜백함수로 전달.
        console.log(sum);
    })
}

add(3,5);
```

- setTimeout(): 설정한 시간에 콜백 함수를 호출하는 함수.
```javascript
setTimeout(callback, 3000);
```
- setInterval(): 타이머(timer)를 설정하고 해당 시간이 지날 때마다 등록된 콜백 함수를 호출하는 함수.<br>
- clearTimeout(): 함수를 호출한 결과로 반환된 ID를 인자로 받아 예약되어 있던 함수 호출을 취소하는 함수.<br>
- clearInterval(): setInterval() 함수를 호출한 결과로 반환된 ID를 인자로 받아 주기적으로 호출되던 함수 호출을 취소하는 함수.<br><br><br>

- 폼 이벤트(Form Event): HTML 문서의 폼 엘리먼트에 변화가 생겼거나 제출(submit) 버튼 등이 눌렸을 때 발생하는 이벤트.<br>
- 윈도 이벤트(Window Event): 페이지가 모두 로드되었을 때 발생하는 이벤트.<br>
- 마우스 이벤트(Mouse Event): 사용자가 마우스를 조작했을 때 발생하는 이벤트.<br>
- 키 이벤트(Key Event): 사용자가 키보드를 조작했을 때 발생하는 이벤트.<br>

    addEventListener(): 다른 이벤트 핸들러를 덮어쓰지 X -> 이벤트 핸들러를 여러 개 추가 가능.<br>
```html
<script>
var t = document.getElementById("form1");
t.onsubmit = function a( ) {
    console.log("from property");
    return false;
}
function b( ) {
        console.log("from addEventListener");
        return false;
    }
    t.addEventListener("submit", b);
</script>
```
    removeEventListener(): 이벤트 핸들러를 삭제.

클로저: 자바스크립트의 함수 + 함수가 선언될 때의 환경
// 정보 은닉과 캡슐화 가능해서 사용?

```javascript
function makeCounterFunction(initVal) {
    var count = initVal;
    function Increase( ) {
        count++;
        console.log(count);
    }
    return Increase;
}

var counter1 = makeCounterFunction(0); // 클로저가 가리키는 함수: function Increase(){}, 클로저의 환경: var count = 0;
var counter2 = makeCounterFunction(10); // 클로저가 가리키는 함수: function Increase(){}, 클로저의 환경: var count = 10;

counter1( );
counter2( );
```

## 프로토타입
---
모든 객체가 공통적으로 가지고 있는 속성.
자바스크립트에서 함수를 생성하면 동시에 생성.
new 키워드로 함수에서 찍어낸 모든 객체들이 이 프로토타입을 참조.

함수를 선언하면 2개의 객체가 생성.
1. function 객체.
2. prototype 객체.

함수에서는 프로토타입 객체에 prototype이라는 내부변수로 접근 가능,
프로토타입에서는 constructor라는 변수로 함수에 접근 가능.

new를 할 경우 this 객체가 생성, 또한 반환되어 새로운 인스턴스에서 해당 객체를 사용할 수 O.

프로토타입 속성을 설정 -> 함수의 인스턴스를 생성 -> 인스턴스에서 프로토타입 값 수정

prototype에서 값을 가져오지만 어디까지나 프로토타입은 인스턴스를 찍어낼 때 참조 가능한 기본값을 가지고 각각의 인스턴스는 프로토타입으로 받은 값을 개별로 사용이 가능하게 된다는 것.

__proto__ 프로퍼티와 prototype 프로퍼티 다른건가?
this 키워드는 f() 함수가 호출되었을 때 어떤 객체에 바인드된 속성으로 호출된 것인지를 보여 줍니다. ???
메서드(method): 함수가 객체의 속성 값이 될 경우의 함수.


## 클래스
---

클래스(생성자함수): 연관있는 변수와 함수 
- 객체 단위의 코드를 그룹화.
- 객체 단위의 중복 코드 제거 및 코드의 재사용성.

일반 함수: 특정기능을 하는 변수 + 구문
- 기능 단위의 코드를 그룹화.
- 기능 단위의 중복 코드 제거 및 코드의 재사용성.

1) 리터럴 방식
```javascript
var 인스턴스 = {
  프로퍼티1 : 초기값,
  프로퍼티2 : 초기값,
  메서드1 : function() {
  },
  메서드2 : function() {
  }
}
```

2) 함수 방식
```javascript
function 클래스이름() {
  this.프로퍼티1 = 초기값;
  this.프로퍼티2 = 초기값;
  this.메서드1 = function() {
  }
  this.메서드2 = function() {
  }
}
var 인스턴스 = new 클래스이름();
```

3) 프로토타입 방식
```javascript
function 클래스이름() {
  this.프로퍼티1 = 초기값;
  this.프로퍼티2 = 초기값;
}
클래스이름.prototype.메서드1 = function() {
}
클래스이름.prototype.메서드2 = function() {
}
```

## 네트워킹
---

> Ajax(Asynchronous Javascript and XML)

: 브라우저에서 페이지를 이동하지 않고 자바스크립트를 통해 HTTP 요청을 보낸 후 그 응답을 받아 처리할 수 있는 기술.

페이지를 이동 없이 서버에서 새로운 정보를 받아 오거나 브라우저의 데이터를 서버로 전달 가능.

```html
<html>
    <head>
        <meta charset = "utf-8">
        <script>
            var req = new XMLHttpRequest( );
            req.open("GET", "./data.txt"); // 첫 번째 인자: GET이나 POST와 같은 HTTP request method, 두 번째 인자: 얻어올 리소스 또는 URL.
            req.send( ); // HTTP 요청을 전송.
        </script>
    </head>
    <body>
        AJAX
    </body>
</html>
```
Network => 타임라인과 파일 목록.
HTML 파일이 먼저 로드 -> data.txt 파일이 XMLHttpRequest로 요청 -> 응답 받음.

 req.response;로 내용 확인 가능.

 해당 요청은 비동기로 요청되고 이후 자바스크립트 코드가 실행.

 동기로 HTTP 요청을 보내기 때문에 send() 메서드로 호출한 후에 바로 response에 접근할 수 X.

ReadyState: 요청 진행 상태에 따라 업데이트.

• 0: open( ) 메서드가 호출되기 전<br>
• 1: open( ) 메서드가 호출된 후<br>
• 2: 보낸 요청에 대해 응답에 헤더가 수신된 후<br>
• 3: 응답 메시지에 body 부분이 수신 중일 때<br>
• 4: 모든 응답이 완료되었을 때

JSON: 자바스크립트의 객체를 문자열로 표현하는 방법.