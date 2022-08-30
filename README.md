/\*
.container {

> ul { // 자식 선택자가 필요한 경우 > 을 붙인다.

    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange;
      }
    }

}
}

// & - 상위 선택자 참조
.btn {
position: absolute;
&.active {
color: red;
}
}

.list {
li {
&:last-child {
margin-right: 0;
}
}
}

.fs {
&-small { font-size: 12px; }
&-medium { font-size: 14px; }
&-large { font-size: 16px; }
}

// 중첩된 속성 -> :
.box {
font: {
weight: bold;
size: 10px;
family: sans-serif;
};
margin: {
top: 10px;
left: 20px;
};
padding: {
top: 10px;
bottom: 40px;
left: 20px;
right: 30px;
};
}

// 변수(Variables)
$size: 300px; // -> 전역변수

.container {
$size2: 200px; // -> 지역변수
position: fixed;
top: $size2;
.item {
$size2: 100px;
width: $size;
height: $size2; // 재할당이 가능하다. -> 100px
transform: translateX(100px);
}
left: $size2; // 재할당이 되어서 값이 변경되었으므로 100px
}

.box {
width: $size2; // -> error: 다른 지역의 변수를 참조할 수 없음
}

// 산술 연산
div {
$size: 30px;
width: 20px + 20px;
height: 40px - 10px;
font-size: 10px \* 2;
margin: $size / 2; // 나누기 연산이 필요할 때는 전체를 소괄호로 감싸거나 변수에 담아 계산하거나 다른 연산자와 같이 쓴다.
padding: 20px % 7;
}
span {
font-size: 10px;
line-height: 10px;
font-family: serif;
font: 10px / 10px serif; // 단축속성 font: font-size / line-height / font-family -> 값이 필수로 들어가야 해서 잘 안쓰임
}
div {
width: 100% - 200px; // error -> calc함수 사용해햐 함
}

// 재활용(Mixins)
// 재활용할 코드 앞에 @mixin 붙이고
// 재활용해서 사용할 코드 앞에 @include를 붙여서 쓴다.
@mixin center {
display: flex;
justify-content: center;
align-items: center;
}
.container {
@include center;
.item {
@include center;
}
}
.box {
@include center;
}
//---------------------------
// 인수를 사용한 mixin, 인수에 기본값을 설정해주면 재활용 시 ()를 쓰지 않아도 됨
@mixin box($size: 100px) {
  width: $size;
  height: $size;
  background-color: tomato;
}
.container {
  @include box(200px);
  .item {
    @include box;
  }
}
.box {
  @include box;
}
// 여러 개의 매개변수들을 가질 수 있다.
@mixin box($size: 80px, $color: tomato) {
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(200px, red);
  .item {
    @include box($color: green); // 키워드인수 -> 인수의 값이 매개변수로 직접 들어갈 수 있어 매개변수의 순서와 갯수를 일치시키지 않아도 된다.
}
}
.box {
@include box;
}

// 반복문
@for $i from 1 through 10 {
  .box:nth-child(#{$i}) { // nth-child() 괄호 안의 부분은 원래 값을 넣는 곳이 아니므로 보간을 사용해서 값을 넣는다.
width: 100px \* $i;
}
}

// 함수
@mixin center {
display: flex;
justify-content: center;
align-items: center;
}

// 화면 비율 등을 계산할 때 유용하다.
@function ratio($size, $ratio) {
@return $size \* $ratio
}

.box {
$width: 160px;
  width: $width;
  height: ratio($width, 9/16);
@include center;
}

// 색상 내장 함수
.box {
$color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &:hover {
    background-color: darken($color, 10%);
}
&.buil-in {
background-color: mix($color, red); // mix($color, red) - 두 색상을 섞어준다.
// lighten($color, 10%); - 10% 더 밝은 색으로
                                          // darken($color, 10%); - 10% 더 어두운 색으로
// saturate($color, 10%); - 10% 더 채도를 올려줌
                                          // desaturate($color, 10%); - 10% 더 채도를 낮춰줌
// rgba($color, .5); - 50%의 투명도를 가짐
                                          // grayscale($color); - 대상을 흑백으로 전환
// invert($color); - 색상 반전
}
}
\*/
