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

```scss
$box-width:300px / 960px * 100%
```

