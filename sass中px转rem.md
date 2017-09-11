
### sass中px转rem
```
@function px2em($px, $base-font-size: 75px) {
  @if (unitless($px)) {
    @warn "Assuming #{$px} to be in pixels, attempting to convert it into pixels for you";
    @return px2em($px + 0px);
    // That may fail.
  } @else if (unit($px) == rem) {
    @return $px; } @return ($px / $base-font-size) * 1rem;

}
```

### scss中px转rem中字体的用法
```
/*
* 字体
* 使用
* @include px2px(font-size,40);
*/
@mixin px2px($name,$px){
  #{$name}:round($px/2)*1px;
  [data-dpr='2'] & {
    #{$name}:$px*1px;
  }
  // for mx3
  [data-dpr="2.5"] & {
    #{$name}: round($px * 2.5 / 2) * 1px;
  }
  // for 小米note
  [data-dpr="2.75"] & {
    #{$name}: round($px * 2.75 / 2) * 1px;
  }
  [data-dpr="3"] & {
    #{$name}: round($px / 2 * 3) * 1px
  }
  // for 三星note4
  [data-dpr="4"] & {
    #{$name}: $px * 2px;
  }
}
```
