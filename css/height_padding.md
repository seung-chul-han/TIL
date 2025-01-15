box-sizing: content;
일 경우 height는 content의 높이만 설정 한다.

box-sizing: border-box;
height는 border + padding + content 값으로 설정 된다.

```css
.box {
 box-sizing: border-box;
height: 0;
padding-top: 30px;
}
```
일 경우 height는 0이지만 padding-top: 30px 값이 추가 되므로 30px의 높이를 갖는다.

```
# mdn
The height CSS property specifies the height of an element. By default, the property defines the height of the content area. If box-sizing is set to border-box, however, it instead determines the height of the border area.
```

[css spec](https://drafts.csswg.org/css-sizing-3/#example-8af7a68e)
