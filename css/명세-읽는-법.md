# 스펙 읽기

## BNF(Backus Naur Form) 배커스 나우르 표기법

### 형식

```
&lt;symbol&gt; ::= __expression__
```

비말단기호 ::= 다음에 오는 것으로 대체 될수 있음. expression 하나 이상의 기호로 이루어져 있으며 왼쪽 항에 오는 의미를 나타냄

즉 위의 뜻은 **왼쪽 항에 있는 symbol 은 오른쪽에 있는 것으로 대체 될 수 있다.**

### 비말단 기호

좀 더 하위 요소로 쪼개질 수 있거나 대체될 수 있는 기호 &lt; 와 &gt; 사이에 쓴다.

### 말단 기호

값이 더 이상 하위 요소로 분해되거나 대체될 수 없음을 나타냄

## css 속성값 문법

css 속성값 구문이 BNF 의 개념에서 비롯한 것이긴 하나 css 에서는 표현식 안의 기호를 **구성값** 이라고 부른다.

```
<line-width> = <length> | thin | medium | thick

#<length>, thin, medium, thick : 구성값
```

### 구성값

#### 구성값의 종류

- 키워드
- 기본 데이터 타입
- 속성 데이터 타입
- 비속성 데이터 타입

**키워드**
따옴표나 화살괄호 없이 쓰는 값. css 에서 쓰던 속성값을 있는 그대로 쓰는것. 이 값들은 더 이상 쪼개지거나 다른 값으로 대체될 수 없기 때문에 말단 기호로 취급됨. 위의 thin, medium, thick 은 전부 키워드 값

**기본 데이터 타입**
실제 길이 단위, 색상 값으로 대체될 수 있으므로 비말단 기호임.

```
<background-color> = <color>

.example { background-color: red; }
.example { background-color: honeydew; }
.example { background-color: rgb(50%,50%,50%); }
.example { background-color: rgba(100%,100%,100%,.5); }
.example { background-color: hsl(280,100%,50%); }
.example { background-color: hsla(280,100%,50%,0.5); }
.example { background-color: transparent; }
```

**속성 데이터 타입**
속성의 실제 이름을 정의하는 비말단 기호로 &lt; 와 &gt; 속성이름으로 나타냄

```
<border-width> = <line-width>{1, 4}

.exam { border-width: 2px; }
```

**비속성 데이터 타입**
자신의 이름을 속성으로 사용하는 것을 허용하지 않는 비말단 기호 그러나 이값은 다른 css 속성의 상태를 정의하기 위해 사용하는 그 자체로는 css 속성이 아니지만, 다양한 속성을 정의하기 위해 사용되는 데이터 타입

```
<line-width> = <length> | thin | medium | thick

<border-width> = <line-width>{1, 4}
```

### 구성값 조합

구성값 사이에 다음과 같은 5 개의 조합자를 넣어 새로운 속성값을 표현할 수 있다.

#### 인접값

만약 일련의 구성값이 쭉 나열되어 있으면 css 에서 속성을 사용하고자 할 때 나열된 순서대로 구성값을 전부 써야 한다. css 작성시 해당 속성 선언문이 유효하려면 나열된 순서대로 속성값을 작성 해야 한다.

```
<property> = val1 val2 val3
.exam { property: val1 val2 val3; }
```

#### 더블 앰퍼센트(&amp;&amp;)

2 개 이상의 값 사이에 &amp;&amp;를 쓰면 이 값들은 반드시 나타나야 함.
그러나 등장 순서는 어떤 것이 먼저 오더라도 상관 없음

```
<property> = val1 && val2
.exam { property: val1 val2; }
.exam { property: val2 val1; }
```

#### 싱글파이프(|)

이 기호로 연결된 값 중에 하나만 나타나야 한다.

```
<property> = val1 | val2 | val3
.exam { property: val1; }
.exam { property: val2; }
.exam { property: val3; }
```

#### 더블파이프(||)

이 기호로 연결된 값 중 순서에 상관없이 하나 이상 써야 한다.

```
<property> = val1 || val2 || val3
.exam { property: val1; }
.exam { property: val2; }
.exam { property: val3; }
.exam { property: val1 val2; }
.exam { property: val1 val2 val3; }
```

#### 대괄호([])

대괄호 기호로 하나이상의 속성값을 감쌀 수 있는데 이 괄호로 감싸진 값들이 하나의 그룹으로 묶였다는 뜻

```
<property> = [val1 | val2] val3
.exam { property: val1 val3; }
.exam { property: val2 val3; }
```

### 구성값 복합자

다음과 같이 8 가지 복합자를 사용해 속성값을 여러번 반복하여 사용 할 수 있다.

#### ?

자신 앞에 오는 값이 옵션값임을 나타냄
앞에 오는 값으 종류로는 타입이나 단어, 혹은 그룹이 있다.
이 기호(?)가 붙은 값은 css 선언문에서 아예 쓰지 않거나 한번만 쓸 수 있다. []안에 ','가 있으므로 val1 과 val2 를 같이 쓰려면
','를 넣어 줘야 한다.

```
<property> = val1 [, val2]?
.exam { property: val1; }
.exam { property: val1, val2; }
```

#### \*

앞에 오는 값인 타입이나 단어, 그룹을 css 선언문에서 아예 안쓰거나 1 번 이상 써도 된다는 것을 뜻함
아래 예시에서 val2 는 몇번이고 반복해서 사용 가능

```
<property> = val1 [, val2]*
.exam { property: val1; }
.exam { property: val1, val2; }
.exam { property: val1, val2, val2; }
```

#### +

앞에 오는 값인 타입이나 단어, 그룹을 css 선언문에서 한번이상 써야 함을 나타냄
이 경우 값을 반복할 때 그 앞에 쉼표를 붙일 필요가 없음.

```
<property> = <val>+
.exam { property: <val>; }
.exam { property: <val> <val>; }
.exam { property: <val> <val> <val>; }
```

#### {A}

타입이나 단어, 그룹 다음에 숫자값을 넣은 중괄호가 붙으면 해당 값이 A 번 반복됨을 뜻함.
아래 예시는 작성한 선언문이 유효하려면 값을 2 번 연달아 써야함.

```
<property> = <val>{2}
.exam { property: <val> <val>; }
```

####{A, B}
해당 값이 최소 A 번에서 최대 B 번 나타남을 뜻함.

```
<property> = <val>{1. 3}
.exam { property: <val>; }
.exam { property: <val> <val>; }
.exam { property: <val> <val> <val>; }
```

#### {A, }

해당 값을 최소 A 번 반복 할 수 있음.
이 경우 최대값은 없으므로 원하는 만큼 반복이 가능
아래 예시는 선언문 작성시 값을 한번은 꼭 써야 하면 한번 쓰고 난뒤에는 몇번이고 추가적인 값을 반복해서 쓸 수 있다.

```
<property> = <val>{1, }
.exam { property: <val>; }
.exam { property: <val> <val>; }
.exam { property: <val> <val> <val>; }
.exam { property: <val> <val> <val> <val>; }
```

#### '#'

해당 값이 1 번 이상 반복됩.
반복값은 ',' 로 구분됨

```
<property> = <val>#
.exam { property: <val>; }
.exam { property: <val>, <val>; }
.exam { property: <val>, <val>, <val>; }
```

#### !

느낌표가 그룹값 다음에 붙으면 적어도 이 그룹에서 값이 하나 이상 나와야 한다.

```
<property> = val1 [val2 | val3]!
.exam { property: val val2; }
.exam { property: val val3; }
```

### e.g.

text-shadow 의 속성값

```
none|[<length>{2, 3} && <color>?]#
```

- |는 키워드인 none 과 그룹 [ ]중에 하나를 쓸 수 있다는 것을 뜻함.
- 구성값 복합자인 #은 그룹 안에 담긴 값을 쉼표로 구분하여 하나 이상 쓸 수 있다.
- 그룹안을 보면 {2, 3}은 길이 값을 2 개에서 3 개 쓸 수 있다.
- &amp;&amp;는 대괄호 그룹 안의 값들을 전부 써야 하나 나열 순서는 상관 없다.
- &lt;color&gt;값은 ? 복합자와 함께 써져 있으므로 이는 이 값을 쓰지 않거나 혹은 한번만 써도 된다.

```
.exam { text-shadow: none; }
.exam { text-shadow: 10px 10px red; }
.exam { text-shadow: red 10px 10px; }
.exam { text-shadow: 10px 10px red, 20px 10px 5px green; }
```
