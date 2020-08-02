# SCSS 변수? variables?

파일 이름 앞에 \_파일이름 이런식으로 언더바를 붙여주면, 이 파일은 css파일로 컴파일이 되지 않는다.
자주 사용하는 속성이나 중요한 속성을 파일로 만들어 놓고 여러군데서 사용하게 하는 것 같다.

선언 방법은 \$속성명 : 속성~~
사용방법은 파일에 임포트를 해야 한다. 가령 이런식으로 -> @import "\_variables";
그런 다음 해당 속성을 변수처럼 사용하면 된다.

# mixins

\_mixin.scss 파일을 만든다음, 그! 파일!에 @mixin 이라 쓰고 코드를 정의하면 된다. @mixin 속성함수명 { css속성1 , 2, 3~ }

사용할땐 style.css 파일에서 @import 한 뒤, 타겟속성의 내부에 @include 해서 사용한다. 즉, h1{ @include mixin네임 } 요런 식으로

위의 변수와 다른점은 이것은 여러 속성을 묶어서 한번에 사용이 가능하다는 것인것 같다. 여러개의 동일한 태그나 동일한 부분을 같은 속성으로 스타일링
하는것에 있어서 굉장히 유용하다.

메소드 사용과 비슷하다. @mixin => function , mixin명 => 함수명, (인수)를 사용하는 것까지.즉 호출시에는

    @include mixin명(인수로 들어갈 속성)

    @mixin mixin명($property){
        width : $property
    }

심지어는 조건문도 가능하다. 호출하는 믹신메소드에 속성값대신 문자열을 넣어서 믹신파일에서 조건문을 통해 해당하는 오브젝트에 적용시키는 것.

    input:nth-child(odd){
        @include 믹신("인수");
    }
    input:nth-child(even){
        @include 믹신("인수");
    }

이건 마치 메소드처럼 함수호출이 된다. 인수는 믹신파일에 전달되어서

    @mixin 믹신($arg){
        ~~~~~~~~~
        @if($arg == "해당값"){
            속성1, 속성2
        }@else{
            속성3, 속성4
        }
    }

# extends

\_가 붙는 파일을 만든 뒤, %를 붙여서 속성명을 만든다. 그런다음 필요한 속성을 입력하고, 사용해야 할 부분에 @extend %이름; 을 써주면 된다.

    %button {
        font : inherit;
        padding : 15px 10px;
        background-color : grey;
        border : none
    }

    a{
        @extend %button;
        text-decoration : none;
    }
    button{
        @extend %button;
        border : none;
        outline : none;
    }

extend와 mixin의 차이점은 mixin은 인수를 사용할수 있기 때문에 내부에서 조건문 작성도 가능하지만, extend는 속성의 덩어리이다.
