# request 요청시 header에 cookie 넣어 보내기

```js
let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: '',
  headers: { 
    'Version': '', 
    'Cookie': 'key=value' // headers에 넣어 주면 된다.
  }
};

axios.request(config)
```
