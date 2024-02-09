## this

```js
class StudyThis {
  foo = 'bar';

  echo() {
    console.log(this.foo);
  }
  execute(func) {
    func();
  }
  executeEcho() {
    this.execute(this.echo);
  }
}

const a = new StudyThis();
a.executeEcho();
```
에서 `Uncaught TypeError: Cannot read properties of undefined (reading foo)`오류가 나는 이유

StudyThis에 있는 메서드들은 prototype method들이다.
따라서 이 메서드들을 호출 하는 방법은 인스턴스로 호출을 해야 된다.
그리고 여기서의 this는 이 메서드들을 가지고 있는 클래스가 아닌 메서드를 호출한 객체 인스턴스 즉 `a`이다.

즉 11번 라인에서 func()호출 했을 때 echo()를 일반 함수로 착각 했기 때문에 undefined일 거라 생각했음.
prototype 메서드인 echo는 a를 잃어 버린 것이므로 this는 undefined가 되는 것이고 그 undefined에서 foo를 찾으로 했던 것 이므로
TypeError이 나는 것이다.
