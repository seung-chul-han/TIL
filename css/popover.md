# popover

- [mdn](https://developer.mozilla.org/en-US/docs/Web/API/Popover_API/Using#using_hint_popover_state)

## 기본 사용

```
<button popovertarget="mypopover">Toggle the popover</button>
<div id="mypopover" popover>Popover content</div>

```

- popovertarget:

  - button attribute
  - 이 속성이 있는 요소를 popover를 제어하는 버튼으로 변경한다.
  - 제어할 popover의 id를 값으로 사용한다.

- popovertargetaction

  - button attribute
  - popover의 값이 auto라도 popovertargetaction을 지정하면 이 값이 우선 적용된다.
  - 컨트롤에 의해 제어되는 팝오버 요소에 대한 수행할 작업을 지정
    - hide
    - show
    - toggle (값을 지정하지 않으면 기본 toggle)

- popover

  - 상위 요소의 위치나 overflow에 영향을 받지 않는 최상위 layer
  - global attribute
  - auto

    - 빈 값일 경우 기본값으로 설정
    - popover 밖을 클릭하면 popover 닫힘
    - esc 클릭시 popover 닫힘
    - 한번에 하나의 팝오버만 표시 첫번째 팝오버가 열려 있을 경우 두번째 팝오버를 열면 첫번째 닫힘
      - 예외 [중첩 팝오버](https://developer.mozilla.org/en-US/docs/Web/API/Popover_API/Using#nested_popovers)

  - hint
    - 팝오버 표시 될때 자동으로 닫히지 않는다.
    - 닫히는 것은 auto와 같다."light dismissed"
    - mouseover / mouseout, focus / blur와 같은 javascript 이벤트에 의해 표시되거나 닫힌다.
    - click 할 경우 열린 팝오버가 "light dismissed" 된다.
  - manual
    - 자동으로 닫히지 않는다.
    - 가벼운 해제 불가능
    - 선언적 show/hide/toggle 버튼 또는 javascript로 닫아야 한다.
    - 여러개의 독립적인 수동 popover를 동시에 표시할 수 있다.

popover 요소는 user agent에 의해 display:none이다.

## CSS 기능

- ::backdrop

  - 팝오버 뒤에 배치되는 전체화면 요소
  - css 효과를 줄 수 있다.

- :popover-open
  - 팝오버 요소가 표시되는 동안 popover요소에 스타일 지정 하는데 사용

**현재는 popover의 위치를 부모요소의 위치에 상대적으로 위치 시킬 수 없다.**
