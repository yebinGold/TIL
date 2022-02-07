# CSS

<br/>

## CSS란?
- Cascading Style Sheets (Design Language)
- 브라우저에게 웹사이트의 **content**가 **어떻게 보여야 하는지** 알려주는 것 (제목은 노란색이고 이 이미지 크기는 ~~야..)
- HTML과 같은 Markup 언어와 함께 사용한다 (절대 따로 사용하는 것이 아님!).
- HTML이 웹사이트를 이루는 뼈대라면 CSS는 그 뼈대를 채워주는 근육 같은 존재이다.
- 즉, HTML 코드에 대한 Visual **Design/Style**을 담당하는 것

<br/>
<br/>

## CSS와 HTML 연결하기
1. html **파일 안에** style 작성하기 (**inline CSS**)
    - HTML의 head 태그 안에 style 태그를 작성한다.

2. style.css 파일을 **따로 작성**하고 **link**로 html과 연결하기 (**external CSS**)
    - html 파일과 css 파일을 분리하여 따로 작성한다.
    - html 파일에서 **link** 태그를 이용하여 css 파일과 연결한다. **(href=”*.css”**)
    - **rel** (relationship) 속성을 작성하여 두 파일 사이의 관계를 설정해준다. (html-css와의 관계에서 css 파일을 **“stylesheet”** 라고 말한다. **rel=”stylesheet”** 라고 적어주면 됨!)
    
- 보통 2번의 방식을 선호한다. 분리된 css 파일을 가지고 있으면 다른 많은 html 파일에서 재사용할 수 있으며, html과 css 코드를 같은 파일 내에 길게 작성하는 것보다 훨씬 보기에 좋다.

<br/>
<br/>

## CSS 코드 작성하기
- 문법
    - css의 역할 = 특정 html 태그(**selector**)를 가리키면서 (pointer) → **속성(property)**을 정해주는 것(색깔, 글씨체, 크기...)
    - 하나의 selector에 대한 속성들을 **중괄호**로 묶어준다.
    - 각 속성들을 작성하는 규칙 ⇒ **속성: 속성 값;** (이때, 속성에 띄어쓰기 x  대쉬(-)로 연결해줄 것!!)
    - CSS에는 수많은 속성들이 있기 때문에 외우려고 하기 보다는 구글링을 활용하자!!
    
    - Selector를 고르는 방법
        - 1. **태그 이름**을 그대로 써주기
            
            말 그대로 HTML 파일에서 쓰는 태그의 이름을 그대로 가져다 쓰는 것 (h1, ol, ul ...)
            
            모든 같은 태그에 공통으로 적용된다.
            
        - 2. **id** 속성 활용하기
            
            selector 부분(중괄호 앞)에 태그 이름 대신 **#id명** 작성하기
            
            → 해당 id를 갖는 태그를 찾아서 그 태그에만 css 코드가 적용된다
            
        - 3. **class** 속성 활용하기
            
            selector 부분(중괄호 앞)에 태그 이름 대신 **.class명** 작성하기
            
            id와 비슷하지만 **여러 element에서 중복으로 사용이 가능**하기 때문에 다수의 element들이 공통의 속성을 효율적으로 공유할 수 있다.
            
            하나의 element가 **여러 class를 가질 수 있다!** (스페이스로 구분) → 코드 중복 최소화(각각의 class에 같은 코드를 반복할 필요 없이 새로운 class를 만들어주면 됨)
            
        
        - 전체 모든 element에 공통으로 속성을 적용하려면 ***{ }**을 사용한다.
        - 여러 selector에 공통의 값을 주고 싶다면 각 selector를 콤마(,)로 묶어준다.
    
    - CSS의 C는 cascading(계단식, 순서대로)을 의미한다. 즉, 브라우저가 위에 있는 코드부터 차례대로 읽는다는 얘기!  그렇기 때문에 같은 selector를 가리키는 코드가 있고, 겹치는 속성이 있다면 가장 아래에 있는 코드가 최종적으로 적용된다. (덮어쓰기)

<br/>
<br/>
  
## Box
- 모든 웹사이트는 **Box 영역**으로 이루어져 있다! 웹사이트를 분할해보면 각 content들의 영역이 나눠지는 것을 볼 수 있음
- 가장 기본적인 box = **div**
    - div의 너비와 높이 속성 style을 작성해주면 box를 만들 수 있다.
    - **box 옆에는 어떤 것도 올 수 없다.** box가 있는 그 한 줄이 온전히 **box의 영역**
    - 그래서 따로 줄바꿈 해주지 않아도 다음 요소가 알아서 아래로 내려간다. (밀려남)
    - **header, main, section, p** 등으로 만들어진 box도 마찬가지!
- **span, a, img ...**
    - box와 달리 바로 옆에 다른 요소들이 올 수 있다.
    - 대표적으로 위의 세 종류가 있고, 나머지는 거의 다 blocks에 해당한다.

<br/>
  
- 이렇게 옆에 다른 요소가 올 수 없는 것 = **Blocks**
- 옆에 다른 요소가 올 수 있는 것 = **Inlines** (in the same line, 한 줄에 같이 쓸 수 있다는 의미)

<br/>
  
## display 속성
  - 기본적으로 blocks의 display 속성은 block / inlines의 display 속성은 inline이다.
  - 각 속성의 디폴트 값을 바꿔주면 **block을 inline으로** 바꾸기 / **inline을 block으로** 바꾸기가 가능하다! <br/>
  **주의)** inline은 너비, 높이 속성을 가질 수 없다  그래서 높이, 너비가 있는 block을 inline으로 바꿔주면 아무것도 안보임
  
  
  - 위 문제를 해결하기 위해서 block의 속성을 inline이 아닌 **inline-block**으로 바꿔주는 방법이 있다. inline-block은 inline이긴 하지만 브라우저가 각각을 block으로 인식하게 만들어 준다! 
  - **BUT** inline-block은 문제가 많다... (정해진 형식이 없어서 각 block들 사이에 default로 공간이 생긴다거나, 반응형 디자인(responsive design)을 지원하지 않아서 창 크기에 따라 형태가 달라지는 등...)
        
    - ⇒ **Flexbox!!!** 엘리먼트의 display를 flex로 설정해주면 box를 원하는 어떤 곳이든 둘 수 있다! (방향, 위치 등 설정 가능)
        - 규칙 1. **부모 요소 element**에 대해서만 명시할 것 (자식 요소는 xx)
            - ex) div 박스의 위치를 옮기고 싶다면 부모에 해당하는 엘리먼트를 flex container로 만들어주어야 한다!
            - → body의 display 속성값을 **flex**로 변경한다. (**display: flex;**) ⇒ 부모 엘리먼트가 자식 요소들의 속성을 제어할 수 있게 됨
        - 규칙 2. 주축(main axis)과 교차축(cross axis)을 기준으로 속성 제어
            - default로 **주축은 수평**, **교차축은 수직**을 나타낸다. (변경 가능)
            - 주축에 있는 item에 적용되는 속성: **justify-content**
            - 교차축에 있는 item에 적용되는 속성: **align-items**, **align-content**
            - align-items를 사용하려면 부모 요소에 height 속성값을 주어야 함! (height 기본값은 자식 요소의 height와 같기 때문에)
            - body에 height를 줄 때 px 대신 **vh**(view height)를 사용하자! (화면 크기에 따라 바뀌는 단위, width는 vw)
        - 규칙 3. 주축과 교차축 (수평/수직)을 바꿔주려면 **flex-direction**을 수정하자
            - flex-direction: **column** or **row** or **reverse**;
            - **row** (**default**) = 주축-수평 교차축-수직 / **column** = 주축-수직 교차축-수평
            - reverse = 순서 반전 (column-reverse 상하 반전 / row-reverse 좌우 반전)
        - 규칙 4. wrapping이 일어나지 않게 하려면 **flex-wrap**을 수정하자
            - flex-wrap: nowrap; ⇒ 모든 요소들을 한 줄에 있게 하기 위해 고정된 width 값이 변경된다.
            - flex-wrap: wrap; ⇒ 요소들의 고정 width값이 유지되고, 화면이 작아질 경우 다음 줄로 넘어간다.
            - flex-wrap: wrap-reverse; ⇒ 화면이 작아질 경우 요소들이 윗줄로 올라간다.
        - 규칙 4. flex-direction과 flex-wrap은 같이 쓰이는 경우가 많기 때문에 **flex-flow**로 한번에 쓸 수도 있다.
            - 문법 = **flex-flow: direction wrap;**
        - 규칙 5. 줄 간격을 지정하고 싶다면 align-items가 아닌 **align-content**를 사용하자
            - space-around, space-between, space-evenly   
        
    - Flexbox 이해를 위한 게임~ -> [Flexbox Froggy](https://flexboxfroggy.com/#ko)

<br/>
<br/>
  
## box의 세가지 CSS 속성: Margin & Border & Padding
- **Margin**: box(content)의 border(경계) 바깥쪽 공간
    - 따로 설정하지 않아도 브라우저가 body에 대한 기본 margin을 설정해준다 (user agent stylesheet) 없애려면 따로 설정해줘야 함 (margin: 0;)
    - margin-top, margin-bottom, margin-left, margin-right가 존재. 그냥 margin을 주면 상하좌우에 전부 적용된다. (값 두 개를 줄 경우 상하/좌우, 네 개를 줄 경우 시계방향 순으로 상/우/하/좌로 적용됨)
    - Collapsing margins: 상하에 해당되는 두 margin 값이 만나는 경우, 더 큰 margin의 값으로 전체에 적용됨. (위아래 margin에서만 적용됨)
- **border**: box(content)의 테두리(경계) 부분
    - **border: 두께(사이즈) 스타일 색;** 으로 작성한다. 하나의 속성값만 변경하고 싶다면 border-style, border-color 등으로 속성 이름을 설정하면 된다.
    - 많은 style이 있지만 보통 **solid** style border만 사용한다. ~~다른 건 너무 못생겨서..~~
    - 다른 스타일들은 mdn 참고하기
    - block과 inline 모두에 적용된다.
- **Padding**: box(content)의 border(경계) 안쪽 공간
    - margin과 같이 상하좌우로 값이 적용됨.
    
- **inline**의 경우 box는 아니지만(width, height 속성 적용 못함), margin과 border, padding 모두 적용 가능하다!
- 다만 inline은 높이와 너비(상하)가 없기 때문에 **margin**의 경우 **좌우에만** 적용된다.
- 그래서 inline 요소에 상하 margin을 주고 싶다면? → display 속성을 block으로 변경해줘야 한다!

<br/>
<br/>
  
## position
- 요소들의 위치를 조금씩 옮기고 싶을 때 사용하는 속성
- position: **static**; ⇒ default
- positon: **fixed**; ⇒ **초기 생성 위치에 고정**됨. 스크롤을 내려도 위치가 유지된다.
    
    고정되는 위치는 수정할 수 있지만(top, left, right, bottom), 수정 후 기존의 위치 속성은 모두 무시된 채 **새로운 다른 레이어** 상에 자리 잡는다. (모든 레이어 중 **가장 위에 위치**하기 때문에 다른 요소들과 겹쳐서 나타날 수 있음)
    
    ex) 웹사이트 최상단의 메뉴바는 스크롤을 내려도 위치가 고정된 채 따라온다 = fixed 
    
- position: **relative**; ⇒ **초기 생성 위치를 기준**으로 상하좌우: px 단위로 이동 한다. (top left bottom right→**세부 위치 조정**)
- position: **absolute**; ⇒ **가장 가까운 relative한 부모 element를 기준**으로 **맨 위/아래/왼쪽/오른쪽**으로 이동한다. (relative한 부모가 없으면 **body를 기준**으로)

<br/>
<br/>
  
## Pseudo Selectors
- element를 **세부적으로** 선택하는 방법 ⇒ **태그 이름: 속성 { }**
- ex) div: first-child { } → 여러 div 중 첫번째 것 / div: last-child{ } → 여러 div 중 마지막 것 <br/>
      div: nth-child(N) { }→ 여러 div 중 N번째 것(odd, even도 선택 가능)  <br/>
      input: required {style} → required 속성을 가지는 input을 select <br/>
- html 코드를 수정할 필요 없이 css 코드에서 선택만 잘 해주면 되므로 효율적인 방법이다.

<br/>
  
## Attribute selector

- 태그가 갖는 attribute를 통해 selector를 선택하는 방법 (class를 지정할 필요 없이 CSS만으로 가능)
- **tag [attr=”value”] {style}** ⇒ 해당 속성값이 value인 tag를 select
    
    **tag [attr~=”value”] {style}** ⇒ 해당 속성값에 “value”(+앞뒤공백)를 포함하는 모든 tag를 select
    
    **tag [attr\*=”value”] {style}** ⇒ 해당 속성값에 value를 포함하는 tag를 select
    
    **tag [attr$=”value”] {style}** ⇒ 해당 속성값이 value로 끝나는 tag를 select
    
    ex) input[type=”text”] { } ⇒ text 타입인 모든 input을 선택
    
    input[placeholder~=”name”] { } ⇒ placeholder에 **단어** “name”을 포함하는 모든 input을 선택 ex) first **name**, last **name**
    
    input[placeholder*=”name”] { } ⇒ placeholder에 “name” **문자열**을 포함하는 모든 input을 선택 ex) abcdefghijklm**name**opqr
    
- 더 많은 속성들→ mdn 참조 [Attribute selectors - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

<br/>
<br/>

## Combinators
- 다른 selector와 함께 쓰이면서 **둘 사이의 관계**를 표현하는 방식의 **selector**
1. **Descendant combinator(space)**: div span {style} ⇒ div(부모) 속에 존재하는 **모든** span(**자식**)을 찾아서 select
2. **Child combinator(>)**: div **>** span {style} ⇒ div의 **direct child** span(바로 밑에 있는 자식)을 찾아서 select
3. **Adjacent sibling combinator(+)**: div **+** span {style} ⇒ div의 **direct brother** span(**형제**)을 찾아서 select (둘 사이에 다른 요소가 있으면 안됨. 무조건 바로 뒤!!)
4. **General** **sibling combinator(~)** : div ~ span {style}  ⇒ div와 형제이기는 하지만 바로 뒤에 오지 않는 형제 span을 찾아서 select

<br/>

- CSS는 기본적으로 Cascading의 우선순위를 갖지만, selector들 간에는 고려해야 할 우선순위가 따로 존재한다.
- selector 우선순위 계산하기 → [Specificity Calculator](https://specificity.keegan.st/)

<br/>
<br/>

## States
- element의 **활성화 상태**에 대한 스타일
1. **: active** ⇒ 대상을 클릭하고 있는 상태
2. **: hover** ⇒ 마우스가 대상 위에 있는 상태 (클릭 아님)
3. **: focus** ⇒ 키보드로 선택되어 있는 상태 (Tap 키 등등)
4. **: visited** ⇒ 링크에 방문한 상태, 링크에만 적용.
5. : **focus-within** ⇒ focused된 자식을 가진 **부모 요소**에 적용됨

- state를 다른 element와 연계해서 사용할 수도 있다.
    - **elem1: state elem2 {style}** ⇒ elem1(부모)가 활성화되면 elem2(자식)의 스타일이 바뀜
    - **elem1: state elem2: state {style}** ⇒ elem1(부모)가 활성화되고, elem2(자식)도 활성화 되면 elem2의 스타일이 바뀜

<br/>
<br/>

## Colors
1. hexadecimal color (16진수 컬러) : 색상 코드 ex) #FF6347
2. rgb(Red Green Blue)
3. rgba(Red Green Blue Alpha): rgb + opacity(투명도%)

<br/>

### Variable (custom property)

- CSS도 프로그래밍 언어처럼 변수를 사용할 수 있다.
- **:root** 요소(모든 document의 뿌리)에 변수 (**—var-name**)를 추가해서 사용 가능
- 색상 코드, border style 등의 스타일을 저장하여 사용할 수 있다. (ex) —main-color)
- 사용할 때는 **var(변수명)**으로 사용
