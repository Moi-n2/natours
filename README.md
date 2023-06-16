# natours
practice demo

[Live deploy](https://moi-n2.github.io/natours/)

## notes:
1. 响应式布局：
    媒体查询 +rem 
```
@mixin respond($breakpoint){
  @if $breakpoint == phone {
    @media only screen and (max-width: 37.5em) { @content };  //600/16px
  }
  @if $breakpoint == tab-port {
    @media only screen and (max-width: 56.25em) { @content };  //900/16px
  }
  @if $breakpoint == tab-land {
    @media only screen and (max-width: 75em) { @content };   //1200/16px
  }
  @if $breakpoint == big-desktop {
    @media only screen and (min-width: 112.5em) { @content };   //1800/16px
  }
}
```
```
html{
  font-size: 62.5%;  //1rem=10px
  @include respond(tab-land) {
    font-size: 56.25%;  //1rem=9px
  }

  @include respond(tab-port) {
    font-size: 50%;
  }

  @include respond(big-desktop) {
    font-size: 75%;  //12/16px 1rem = 12px
  }
}
```
float+calc() 定义col宽度
```
.row{
  max-width: $grid-width;
  margin: 0 auto;

@include clearfix;

  [class^="col-"] {
    float: left;

    &:not(:last-child) {
      margin-right: $gutter-horizontal;
.col-1-of-2 {
    width:calc((100% - #{$gutter-horizontal}) /2);
  }
  
  .col-1-of-3 {
    width:calc((100% - 2 * #{$gutter-horizontal}) /3);
  }
  
  .col-1-of-4 {
    width:calc((100% - 3 * #{$gutter-horizontal}) /4);
  }

  .col-2-of-3 {
    width:calc(2 * (100% - 2 * #{$gutter-horizontal}) /3) + #{$gutter-horizontal};
  }
  
  .col-2-of-4 {
    width:calc(2 * (100% - 3 * #{$gutter-horizontal}) /4) + #{$gutter-horizontal};
  }

  .col-3-of-4 {
    width:calc(3 * (100% - 3 * #{$gutter-horizontal}) /4) + 2 * #{$gutter-horizontal};
  }
}
```


2. 过度色背景+折角clip-path
```
background-image: linear-gradient(to right bottom, rgba($color-primary-light,0.8), rgba($color-primary-dark,0.8)),url(../../img/hero-small.jpg);
background-size: cover;

clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
```

3. 标题文本background-clip
```
@mixin back-clip{
  background-image: linear-gradient(to right, rgba($color-primary-light,0.8),rgba($color-primary-dark,0.8));
  -webkit-background-clip: text;
  color: transparent;
}

&:hover{
    transform: skewY(2deg) skewX(15deg) scale(1.1);}
```



4.翻转卡片 perspective + rotate

```
.card{
  perspective: 150rem;
  &-base{
    backface-visibility: hidden;
  &-back{
    transform: rotateY(180deg);
  }}}
```

5. 视频背景
```
 <video autoplay muted loop>
    <source src="img/video.mp4" type="video/mp4">
    <source src="img/video.webm" type="video/webm">
    Your browser is not supported!
 </video>

.bg-video{
    position: absolute;
    top:0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: -1;
    opacity: .15;
    overflow: hidden;

    video{
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
```

6. 文本环绕 + 图片滤镜
```
figure{
  float: left;
  shape-outside: circle(50% at 50% 50%);
  clip-path: circle(50% at 50% 50%);
}

img{
  filter: blur(3px) brightness(80%);}
```

7. img-set:
   outline +position => float
```
img{
  outline-offset: 2rem;
  outline: 1.5rem solid $color-primary;
}
```

8.btn hover效果
```
&::after{
    content: '';
    background-color: $color-white;
    display: inline-block;
    height: 100%;
    width:100%;
    border-radius: 10rem;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    transition: all .4s;
  }

  &:hover{
    transform: translateY(-3px);
    box-shadow: 0 1rem 1.5rem rgba(black, 0.2);

    &::after{
      transform: scaleX(1.4) scaleY(1.6);
      opacity: 0;
    }
  }
```

9. form-input输入文本坠落效果
```
&-input:placeholder-shown + &-label{
    opacity: 0;
    visibility: hidden;
    transform: translateY(-4rem);
  }
```

10. input:checked + label:for 自定义表单选项、实现navigation切换效果
11. 兄弟选择器：~后一个节点可在前一个结点的任意位置的兄弟节点；
               + 紧邻在前一个结点之后
12. popup
    通过a:href定位
```
<a href="#popup" class="btn">
    Book now!
</a>

<div class="popup" id="popup">
...
</div>
```









