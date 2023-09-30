# contain
컨텐츠가 넘칠때 스크롤이 생기지 않도록 하는 방법 중 하나는 `overflow: hidden`이 있지만 이 방법으로는 `position: sticky`같은 
속성이 무효화 될 수 있다.
`contain: layout | paint`이 적용된 요소는 새로운 containing block요소가 된다. 하지만 position: sticky에는 영향을 미치지 않는다.

contain: layout은 새로운 containing block을 갖게 되어 이 요소 하위의 요소에 float이 있더라고 다른 위치의 요소에 영향을 주지 않는다.
또한 이 하위요소로 position: fixed요소가 있으면 contain:layout을 같는 요소를 컨터에너로 사용하게 된다.
[mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/contain)
