# [focus-within](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-within)

:focus-within
psudo element 또는 자식 / 자손 요소가 focus 되어 있을 경우를 나타 낸다

```html
<div class="box>
  <input type="checkbox" />
  <span>hello</span>
</div>
```

```css
.box:focus-within {
  background: green;
}

.box:focus-within > span {
  color: red;
}
```

![image](https://github.com/fireworks80/TIL/assets/8033966/917abbe5-5982-47ca-a148-b4948ce4ca84)
