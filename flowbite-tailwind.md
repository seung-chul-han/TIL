# 디자인 토큰 세팅

[flowbote color](https://flowbite.com/docs/customize/colors/)

`tailwind.config.js`의 `theme`의 값을 설정 하면 된다.
tailwind의 값으로 설정이 되어 있으므로 design token에서 설정한 값으로 변경 할 수 없는 것으로 보인다.

```json
// token.json

...
 "blue": {
      "100": {
        "value": "#d4e2fc",
        "type": "color"
      },
      "200": {
        "value": "#a9c5f9",
        "type": "color"
      },
...

```

```json
// tailwind.config.js

 theme: {
        extend: {
            colors: {
// 아래와 같은 형식 변경이 필요
                white: 'red',
                blue: {
                    100: {
                        value: '#d4e2fc',
                        type: 'color',
                    },
                    200: '#a9c5f9',
                    300: '#7da8f7',
                    700: '#174291',
                },
            },
```
