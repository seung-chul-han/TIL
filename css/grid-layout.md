# minmax
```css
minmax(340px, 1fr);
```
최소 340px 최대 1fr 사이에서 유연하게 값을 처리한다.

```html
<div class="wrap">
  <div></div>
  <div></div>
  <div></div>
</div>
```

```css
.wrap {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
}
```
위 코드는

```css
.wrap {
  display: flex;

  & > * {
   flex: 1;
  }
}

@media (max-width: 640px) {
  .wrap {
    flex-direction: column;

    & > div {
      min-width: 340px;
    }
  }
}
```
와 같다.
