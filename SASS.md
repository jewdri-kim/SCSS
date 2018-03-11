# SASS

- SASS는 Syntactically Awesome Style Sheet라는 단어의 줄임말.


- CSS pre-processor로서, 복잡한 작업을 쉽게 할 수 있게 해주고, 코드의 재활용성을 높여줄뿐 아니라, 코드의 가독성을 높여준다. 

[^CSS pre-processor]: css를 확장하는 스크립팅 언어로서, 컴파일러를 통하여 브라우저에서 사용할 수 있는 일반 CSS 문법 형태로 변환한다.



## SASS VS SCSS

- 두 개의 차이점은 문법의 차이가 있다 (문장양식 중괄호와 세미콜론의 유무)
- SASS 파일은 중괄호와 세미콜론이 존재하지 않고, SCSS는 존재한다.
- SASS 문법은 CSS문법과 많이 달라 차후 CSS문법과 거의 흡사한 SCSS문법으로 바뀌었다.

### SASS

```scss
$font-stack: Helvetica, sans-serif 
$primary-color: #333

body 
  font: 100% $font-stack
  color: $primary-color
```

#### SASS의 장점

1. 문법이 간결하다. ( ex: 세미콜론과 중괄호 없음, @include 대신 + 를 사용)
2. 읽기 쉽다. But, 인덴테이션 룰이 스트릭트해서 작성하기는 어렵다.
3. 세미콜론이 없어도 에러안난다. (자동으로 인식)



### SCSS

```scss
$font-stack: Helvetica, sans-serif; 
$primary-color: #333; 

body { 
  font: 100% $font-stack;
  color: $primary-color;
}
```

#### SCSS의 장점

1. 더 표현적이다. (무슨말인지 ? - - attribute/value 의 쌍들을 한줄에 쓸수있다.)
2. 고유한 nesting(중첩)을 장려한다. selector에 이름을 만들어 element명을 변경할 때 관리가 쉽다. (한번에 여러군데 변경가능)
3. 더 모듈화된 코드 장려 @extend  사용
4. 더 나은 인라인 문서를 작성하게 한다. (괄호가 코드와 코멘트를 그룹해준다)
5. css 툴들은  scss에서도 종종 사용가능하다. 
6. **css 와 통합하기가 훨씬 쉽다.**
7. 진입장벽이 낮다.
8. css의 다른 버전이 될수 있다. 



## SASS 컴파일러

사스의 포멧으로만들어진 파일을 css로 변환해주는 도구

SASS 컴파일러는 --watch 옵션을 통해서 사스파일을 감시하다가 그 파일이 수정되면 자동으로 css 로 변환해주기 때문에 html에서는 컴파일된 css를 인클루드해서 페이지가 잘 렌더링 되는지 확인하고, 이 css 파일을 그대로 서버에 반영하면 된다.



여기서! sass파일은 에러가 나면 기존에 있던 css파일 모두 실행이 안됩니다. 

![http://gscdn.hackers.co.kr/publish/img/img1.jpg]()



### 윈도우에서 설치

1. <http://rubyinstaller.org/> 에 방문해서 ruby를 설치한다.
2.  윈도우 + R 키를 누르고  cmd를 입력한다.
3. gem install sass 를 입력해서 sass 컴파일러를 설치한다. 

맥과 리눅스에서는 ruby가 설치되어있어, 그냥 3번을 바로 

사용법과 셋팅은 검색으로...



그냥 공부만 하거나, 예제를 만들어 공유는 [Sassmeister](http://www.sassmeister.com/) 를 사용하는것을 추천!



## 변수 (Variable)

- 변수로 사용 가능한 형태 : 숫자, 문자열, 폰트, 색상, null, lists, maps
- 변수를 사용할 때는 $ 문자를 사용

```scss
$primary-color:#333;
```

변수를 만들어도, 사용하지 않으면 컴파일된 CSS파일에는 아무것도 나타나지 않는다.

### body에서 사용

#### SCSS

```scss
$primary-color:#333;

body{
    background-color:$primary-color;
}
```

#### CSS

```
body{
    background-color:#333;
}
```



### 변수범위(Variable Scope)

sass 의 변수엔 변수범위가 있다. 

변수를 특정 선택자(selecor)에서 선언하면 해당  selector에서만 접근이 가능하다.

#### SCSS

```scss
$primary-color:#333;

body{
    $primary-color:#eee;
    background-color:$primary-color;
}

p{
    color:$primary-color;
}
```

#### CSS

```
body{
    background-color:#eee;
}
p{
    color:#333;
}
```

변수의 값을 global(전역)으로 설정할 때는 `!global` 플래그를 사용한다.

####SCSS

```scss
$primary-color:#333;
body{
    $primary-color:#eee !global;
    background-color:$primary-color;
}
p{
    color:$primary-color;
}
```

#### CSS

```css
body {
  background-color: #eee;
}

p {
  color: #eee;
}
```

추가적으로 `!default` 플래그는 해당 변수가 설정되지 않았거나 값이 null 일때 값을 설정한다.

이 플래그는 나중에 **mixin** 을 작성할 때 유용하게 사용한다. (mixin에 대한 설명은 나중에)

#### SCSS

```scss
$primary-color:#333;
$primary-color:#eee !default;

p{color:$primary-color}
```

#### CSS

```css
p{color:#333;}
```

#### SCSS

```scss
$primary-color:#eee !default;

p{color:$primary-color}
```

#### CSS

```css
p{color:#eee;}
```



## 수학연산자 (Math Operators)

sass 에서는 수학연산자들을 사용할 수 있다. 

ex ) 색상 혼합 기능도 가능하다. white 와 black를 혼합하면 gray. 

지원되는 연산자들은 다음과 같다. 

| Operator |  Description   |
| :------: | :------------: |
|    +     |    addition    |
|    -     |  subtraction   |
|    /     |    division    |
|    *     | multiplication |
|    %     |     modulo     |
|    ==    |    equality    |
|    !=    |   inequality   |

**주의** : `+`, `-` operator 를 사용할 때 단위를 통일해야함

  ex ) 오류발생 

```scss
$box-width:100% -20px
```

이런 작업시에는 css의 `calc()` 함수를 사용해야 한다.

calc()함수 사용법 -> <https://www.w3schools.com/cssref/func_calc.asp>

아래와 같은 식은 오류없이 작동한다.

#### SCSS

```scss
/*$primary-color:#333;*/
$primary-color:#333 !default;

div{width:360px / 960px * 100%;background:$primary-color} 
```

####CSS

```css
div {
  width: 37.5%;
  background: #333; 
}
```

####SCSS

```scss
#navbar{
    $navbar-width:1000px;
    $items:5;

    li{
        width: $navbar-width/$items - 10px;
    }
}
```

####CSS

```css
#navbar li {
  width: 190px; }
```

####SCSS

```scss
h1{
    color:#333 + #111;
    border-color:#023012*2;
    background-color:rgba( 255, 0, 0, 0.75 ) + rgba( 0, 100, 100, 0.75 );
}
```

####CSS

```css
h1 {
  color: #444444;
  border-color: #046024;
  background-color: rgba(255, 100, 100, 0.75); }
```

#### ※단위

- 단위를 숫자에 붙이기 위해서는, 숫자에 1단위를 곱해야 한다

$value:4;

.baa{font-size:$value*1em;} -> .baa{font-size:4em;}

- 단위를 숫자에 붙이기 위해서는, + 단위도 사용가능 

$value:10;

.baa{font-size:$value/1px;} -> .baa{font-size:10}



## 중첩(Nesting)

```wo
HTML 코딩을 하다보면, 중첩적인 표현을 위해 하위 선택자를 많이 사용할 수 밖에 없다.
예를 들어, nav 태그를 이용해서 네비게이션을 만들 때 ul 과 li 라는 태그 선택자가 있는데, 이 두 선택자는 nav의 하위선택자이다. 
```

#### SCSS

```scss
.container{
    width:100%;
    h1{color:red;}
}
```

#### CSS

```css
.container{
    width:100%
}
.container h1{color:red;}
```

- 부모선택자를 리퍼런스 할때는 &문자를 사용합니다.

#### SCSS

```scss
a{
    color:black;
    &:hover{
        text-decoration:underline;
        color:gray;
    }
    &visited{
        color:purple
    }
}
```

#### CSS

```css
a{
    color:black;
}
a:hover{
    text-decoration:underline;
    color:gray;
}
a:visited{
    color:purple
}
```

#### SCSS

```scss
.funky{
    font{
        family: fantasy;
        size:30em;
        wegihit:bold
    }
}
```

#### CSS

```css
.funky{
    font-family:fantasy;
    font-size:30em;
    font-weight:bold;
}
```

※인셉션 규칙 : http://thesassway.com/beginner/the-inception-rule



## 함수(Functions)

- 함수를 이용해서 좌표 또는 색상을 동적으로 변경할 수 있다. 


- 함수 : [lightness](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#lighten-instance_method), [hue](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#adjust_hue-instance_method), [saturation](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#saturate-instance_method), [기타](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)

#### SCSS

```scss
#navbar{
    $navbar-width:800px;
    $items:5;
    $navbar-color:#ce4dd6;

    width: $navbar-width;
    border-bottom:2px solid $navbar-color;
    
    li{
        float:left;
        width:$navbar-width/$items - 10px;

        background-color:lighten($navbar-color, 20%);
        &:hover{
            background-color:lighten($navbar-color, 10%);
        }
    }
}
```

#### CSS

```css
#navbar {
  width: 800px;
  border-bottom: 2px solid #ce4dd6; }
  #navbar li {
    float: left;
    width: 150px;
    background-color: #e5a0e9; }
    #navbar li:hover {
      background-color: #d976e0; }
```

색깔에 관한 함수들의 **보이는 **예제는 [Jackie Balzer 의 Visual Guide to Sass & Compass Color Functions](http://jackiebalzer.com/color) 에서 확인 할 수 있다.



## 불러오기 (Import)

import 기능은 스타일들을 여러파일들로 나누고, 다른파일에서 불러와서 사용하는 기능이다.

다음과 같이 @import directive를 사용하여 특정 .scss 파일을 불러올 수 있다.

```scss
@import "layout.scss";
```

참고로, 확장자를 붙이지않아도 된다.

```scss
@import "layout"
```

- css 는 @import 명령을 지원하는데, 이 명령은 별도의 파일을 네트워크를 통해서 로딩하는 것인데, 네트워크 커넥션은 느리고 비싼 행위다. 
- sass 에서 import는 그 파일의 내용을 실제로 가져와서 파일에 통합한다.
- sass는 import를 위한 이름규칙이 있다. partials라고 불리고 아래에서 설명.

### Partial

만약에 .sass 파일이나 .scss 파일의 이름을 `_` 로 시작하면 css파일로 따로 컴파일되지 않는다.

html 에서 해당 css파일을 불러올 일이 없고, import만 되는경우에 이 기능을 사용한다. 



- scss를 부분화하여 쓸때 import 하여 불러오기를 한 후, 컴파일 과정을 거쳐, 하나의 css파일로 변환하는 것이다. 


- 변수로 처리한 부분만 따로 두는 방법도 SASS의 장점 


- 부분화 파일에는 `_(언더바)` 추가 
- 부분화를 할 때는 파일명 앞에 _(언더바)를 붙이지만, import를 할 때는 `_(언더바)`를 붙이지 않는다. 



## 상속(Extend)

sass 에서 특정선택자를 상속할 때, @extend directive를 사용한다.

####SCSS

```scss
.box{
    border:1px solid #eee;
    padding:10px;
    display:inline-block;
}

.success-box{
    @extend .box;
    border:1px solid #00f;
}
```

#### CSS

```css
.box, .success-box {
    border: 1px solid #eee;
    padding: 10px;
    display: inline-block; }

.success-box {
    border: 1px solid #00f; }
```

### placeholder

Placeholder 선택자 %를 사용하면 상속은 할 수 있지만 해당 선택자는 컴파일 되지 않는다.

#### SCSS

```scss
%box{
    padding:0.5em;
}

.success-box{
    @extend %box;
    color: green;
}

.error-box{
    @extend %box;
    color:red;
}
```



## 믹스인(Mixins)

- 믹스인은 반본적인 속성을 손쉽게 처리할 수 있는 역할을 한다.
- 선택자와 속성을 재활용할 수 있도록 해주는 방법이다. 선언할 때는 '@mixin'으로 시작하고, 호출할 때는 '@include'을 사용한다
- 예로 브라우저 접두사를 붙일때 사용한다.

#### SCSS

```scss
@mixin border-radius($radius){
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box{
    width:300px;
    height:100px;
    border:1px solid #eee;
    @include border-radius(10px);
}
```

#### CSS

```css
.box {
  width: 300px;
  height: 100px;
  border: 1px solid #eee;
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px; }
```



### Interpolation & Mixins

- '#{}'를 사용해서 변수로 속성이나 선택자의 이름을 동적으로 치환할 수 있다.

#### SCSS

```scss
@mixin rounded-top{
    $side: top;
    $radius: 10px;

    border-#{$side}-radius: $radius;
	-moz-border-radius-#{$side}: $radius;
	-webkit-border-#{$side}-radius: $radius;
}

#navbar li { @include rounded-top;}
#footer{ @include rounded-top;}
```

#### CSS

```css
#navbar li {
  border-top-radius: 10px;
  -moz-border-radius-top: 10px;
  -webkit-border-top-radius: 10px; }

#footer {
  border-top-radius: 10px;
  -moz-border-radius-top: 10px;
  -webkit-border-top-radius: 10px; }
```



### 인자(Arguments)

mixin의 진정한 힘은 인자를 통해서 나타나는데, 

인자는 Mixin 안에서만 사용되는  지역변수를 의미한다. 인자는 기본값을 가질수 있다.

#### SCSS

```scss
@mixin rounded($side, $radius: 10px){
    border-#{$side}-radius: $radius;
    -moz-border-radius-#{$side}: $radius;
    -webkit-border-#{$side}-radius: $radius;
}

#navbar li { @include rounded(top);}
#footer { @include rounded(top, 5px);}
#sidebar { @include rounded(left,8px);}
```

#### CSS

```css
#navbar li {
  border-top-radius: 10px;
  -moz-border-radius-top: 10px;
  -webkit-border-top-radius: 10px; }

#footer {
  border-top-radius: 5px;
  -moz-border-radius-top: 5px;
  -webkit-border-top-radius: 5px; }

#sidebar {
  border-left-radius: 8px;
  -moz-border-radius-left: 8px;
  -webkit-border-left-radius: 8px; }
```



Mixin 을 응용하면 이런식으로도 사용가능하다.

### SCSS

```scss
@mixin media($queryString){
    @media #{$queryString}{
        @content;
    }
}

.container{
    width:900px;
    @include media("(max-width: 767px)"){
        width:100%;
    }
}
```

#### CSS

```css
.container {
  width: 900px; }
  @media (max-width: 767px) {
    .container {
      width: 100%; } }
```

