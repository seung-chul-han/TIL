# Javascript 

## 변수
메모리 공간에 저장한 값을 사용할때 쓰이는 메모리의 주소 대신 사용하는 이름

    var 변수명 = 값;
    
    var a;
    a = 1;

    var a, b;

    a = 1;
    b = 2l;

    var a = 1,
        b = 2;

### 변수의 종류
- 전역변수: 프로그램 전체에 걸쳐서 사용되는 변수, 지양, 제일 바깥범위 (전역함수 안에 포함되지 않는)에 변수를 만드는것, window객체의 변수(속성)를 만드는것.
- 지역변수: 스코프라는 특정 지역에서만 사용되는 변수, js에서 스코프는 {}스코프가 아닌 함수 스코프를 갖는다. 즉 함수 안에서 생성된 번수를 지역변수라고 한다. 단 var를 빼먹으면 안됨.
- 매개변수: - 파라미터: 함수의 내부로 전달되는 변수
         - 아규먼트: 함수로 전달하는 값
- 맴버변수: 객체의 정보를 담는 변수

### 주의사항
- 숫자로 시작하면 안됨
- 대소문자 구분
- 변수는 대문자가 아닌 소문자로 시작
- 상수는 모두 대문자로
- 단어 조합시 카멜케이스로
- 예약어(키워드)는 사용하면 안됨

### 상수
절대 변해서는 안되는 값

### 변수명 스타일
- userName
- user_name
- username

## 데이터 종류
- number
- string
- boolean
- function
- undefined
- object
- null

### number
- 10진수 자연수
- 1.23 실수
- 0xffcd 16진수

### string
'abc' 또는 "멍멍이" 같은 따옴표로 감싼 문자열

### boolean
true / false

### function
function 함수명() {}

### undefined
변수 선언후 값을 대입 하지 않았거나
함수의 리턴 값이 없을때

    var a;
    console.log(a); // undefined

### null
객체 값이 존재하지 않는다.
null의 타입은 null이 되어야 하지만 ECMAScript의 버그로 object가 된다.

## 주석
- // (한줄주석)
- /*
        
    (여러줄 주석)

  */ 


## 배열
같은 종류의 데이터(변수값)을 일정한 순서로 담을 수 있음
    
    var userName1 = '영희';
    var userName2 = '출수';
    var userName3 = '철구';
    var userName4 = '맹구';
    var userName5 = '보라';
    var userName6 = '희선';

    // array
    // 같은 종류의 데이터들을 각각의 변수에 담지 않고 userNames라는 
    // 공통된 변수명으로 배열이라는 자료형 안에 담는다.
    var userNames = ['영희', '출수', '철구', '맹구', '보라', '희선'];

### 생성방법
    var 배열명 = []; 

### 접근방법
방번호는 배열의 index를 나타내고 값은 0번부터 배열의 크기 -1까지의 값을 가진다.

    배열명[방번호];

    userNames[0]; // 영희
    userNames[1]; // 출수
    userNames[2]; // 철구
    userNames[3]; // 맹구
    userNames[4]; // 보라
    userNames[5]; // 희선

## 연산자
+, -, *. /, %

### 문자연산
    var userName = '한' + '승철';
    console.log(userName); // '한승철'
    
    // 숫자와 문저연산은 숫자를 문자로 변경해서 연산을 한다. 
    - 1 + '2'; // '12'
    - '2' + 2; // '22'

### 복합 연산
    var a += 2; -> a = a + 2;
    var a -= 3; -> a = a - 3;
    var a *= 3; -> a = a * 3;
    var a /= 3; -> a = a / 3;
    var a %= 3; -> a = a % 3;

### 증감연산
- ++a, a++
- --a, a--

## scope

### 스코프(scope)

함수안에 선언된 변수는 함수 외부에서 접근할 수 없음

    function me() {
        var x = 'local';
    }

    console.log(x); // ReferenceError: x is not defined
                    // 함수 스코프를 같기 때문에 외부에서 me()함수 안의 변수에 접근 할 수 없다.

### 스코프 체인
내부함수 에서는 외부함수의 변수에 접근이 가능하지만 위에서 말한바와 같이 외부에서는 내부 함수의 변수에 접근이 불가능 그리고 모든 함수들은 전역 객체에 접근 할 수 있음.
    
    var out = 'global';
    function outer() {
        console.log('out: ' + out); // global
        function inner() {
            var enemy = 'inner';
            console.log('inner: ' + out); // global
        }
        inner();
    }
    outer();

inner함수는 자기자신의 스코프에서 out번수를 찾는다 없다면 한단계 올라가 outer함수에서 out번수를 찾는다 여기서도 찾지 못하면 다시 한단계 또 올라간다. out변수를 찾기 위해 최상위 스코프인 전역스코프로 올라가도 해당 변수를 찾지 못하면 out is not defined 를 발생한다. 

### 렉시컬 스코핑(lexical scoping)
스코프는 함수를 호출할때가 아니라 **선언** 할때 생긴다.
**정적스코프**라고도 불린다.

    var g = 'gloval';
    var f = function(k, h) {
        var v1, v2;
        console.log(k, h, v1, v2);
        // g, f, k, h, v1, v2 인식가능
    };
    // g, f 만 인식가능

f함수 scope안에서 접근 가능: 외부의  g,f와 내부의 k,h,v1,v2변수 모두 접근 가능
외부 scope에서 접근 가능: g, f

**lexical이란**
인식가능한 변수

**lexical인식 범위**
scope에 따라 조정된다 **scope = lexical Environment**
(scope가 안쪽으로 들어갈 수록 인식범위가 커진다 = 바깥쪽 보다 접근 할 수 있는 변수가 많아진다.)

전역변수를 최소화 = **네임스페이스**를 만든다.

    var obj = {
        x: 'local',
        say: function() {
            this.x;
        }
    };

obj.x, obj.say()로 접근 하기 때문에 다른 변수명과 겹치지 않는다.
하지만 obj.x로 외부에서 접근이 가능함. 

## 캡슐화 / 은닉

- 은닉: 말 그대로 감춘다 (외부에서 접근을 못하도록)
- 캡슐화: 실제로 함수가 실행하는 일은 복잡하다. 이렇게 복잡한부분은 사용자가 알아야 할 필요가 없으므로 복잡한 행동을 숨기고 단순한 행동(인터페이스)만 노출하는것.
ex) 계좌이체: 내가 하는 일 - 계좌번호 누르기, 이체 실행(캡슐화)
            실제 일어나는일 - 해당 계좌가 있는가, 어느 지점에서 개설 했는가, 입금액은 얼마인가, 누구에게 보내나 등등

### IIFE (Immediately Invoked Function Expression)
즉시 호출 함수 표현식(모듈패턴)
함수를 선언하자마자 실행

    var scope = (function() {
        var local = 'local'; // 외부에서 local 번수에 직접 접근할 방법이 없다.
        return {
            say: function() {
                console.log(local);
            }
        }
    } ());

    scope.say(); // local - scope.say()를 통해서만 local변수에 접근 할 수 있다.

## @ 싱글턴, 모듈, 생성자

### 모듈패턴
IIFE

### 싱글턴
인스턴스가 사용될 때 똑같은 인스턴스를 만들어 내는 것이 아니라 동일 인스턴스를 사용하는 것.
단하나의 인스턴스를 만든다.

**객체 리터럴**이 싱글턴 패턴의 대표적인 예

객체리터럴
장점: 만들기 쉽다.
단점: 모든 속성이 다 공개 되어 있다.
    
    var obj = {
        a: 'hello',
        say: function() {
            console.log(this.a);
        }
    };

공개된 속성을 비공개로 만들기

    var singleton = (function() {
        var instance = null;
        var a = 'hello';

        function init() {
            return {
                a: a,
                say: function() {
                    console.log(this.a);
                }
            }; // return
        } // init

        return {
            getInstance: function() {
                if (!instance) {
                    instance = init();
                }

                return instance;
            }
        };
    }());

    var fist = singleton.getInstance();
    var sec = singleton.getInstance();
    console.log(fist === sec) // true

getInstance메서드를 보면 instance가 있으면 init()를 거치지 않고 바로 instance를 반환한다.

**언제 써야 하나**

서버측 언어에서 각 요청에 대해 둘 이상의 데이터베이스 연결을 만드는 것이 리소스 낭비기 때문에 연결을 처리하는데 싱글톤을 사용할 수 있다.

프론트엔드에서는 모든 ajax요청을 처리하는 객체를 매번 생성하는 것이 아니라 싱글톤으로 만들 수 있다.