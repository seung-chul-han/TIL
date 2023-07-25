# currentColor
요소의 color 속성값을 나타낸다.

```html
<!-- p의 border color는 blue -->
<p style="border: 4px solid currentColor; color: blue;">
  hello
  <!-- 
    color는 inherit되는 속성이므로
    span의 background color는 blue 
  -->
  <span style="background-color: currentColor;">bello</span>
</p>


```
