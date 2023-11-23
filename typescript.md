`type 'string' is not assignable to parameter of type '""'.ts(2345)`

문자열 값은 `''` 에 할당 할 수 없다는 뜻

```ts
const a = {
  key: ''
} as const;

setValue(a.key, 'h');
상수로 지정을 해놨기 때문에 key에 해당하는 값은 '' 이므로 문자열과 다르다 그래서 위의 오류가 발생
```


```js
const a = {
  key: ''
};

setValue(a.key, 'h');

```
