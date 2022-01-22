# HTML

<br/>

## HTML이란?
- HyperText Markup Language
- 웹사이트의 **contents**(title, text, image, link, etc.)에 대한 정보를 다루는 언어
- 브라우저는 인간의 언어를 이해하지 못하기 때문에 우리가 원하는 content 역시 이해하지 못한다.. 그래서 브라우저에게 content에 대해서 알려줘야만 하는데, HTML을 통해 브라우저에게 content의 구조/구성에 대해 설명할 수 있다!
- 즉, 브라우저에게 웹사이트의 **content**가 **무엇인지** 알려주는 것 (이게 제목이고, 이게 링크야..)

<br/>
<br/>

## 파일 만들기
- 반드시 프로젝트 폴더와 파일 위치를 같게 해주어야 함!
- 폴더/파일명을 작성할 때 항상 **소문자**를 사용하자. (같은 폴더 내에 철자는 같고 대소문자만 다른 파일이 존재할 경우, 브라우저에서 이를 혼동할 수 있다.)

- HTML 파일을 **브라우저**에서 열어주면 웹사이트를 확인할 수 있다.
- 브라우저는 오류가 없다.. 즉, HTML 문법을 따르지 않더라도 브라우저는 항상 우리가 작성한 contents를 보여준다. 문제는 HTML 파일에 오류가 있더라도, 브라우저는 이를 알려주지 못한다는 점이다. 이는 전달 받은 내용을 그대로 보여주려는 브라우저의 가장 큰 특징!

<br/>
<br/>

## 구조
- html은 크게 **Head**와 **Body**로 구성되어 있으며, 각 코드들은 모두 **태그 tag**로 이루어져 있다.
- **head** = 웹사이트의 환경 설정을 담당하는 부분. 외부적으로 보여지지 않음
    - ex) title: 웹사이트의 이름을 설정해 줌, meta: 웹사이트에 대한 부가 정보 제공

- **body** = 웹사이트의 content를 담당하는 부분. 사용자가 볼 수 있는 내용을 작성함

- **작성 규칙**
    - 모든 html 파일의 첫 줄은 **!DOCTYPE html**로 시작한다. → 브라우저에게 html파일임을 알려줌
    - **html** 태그를 작성, 이 안에 작성하는 모든 것들이 html 코드가 된다.
    - **head**와 **body** 태그를 열어줌, 그 안에서 각각의 코드를 작성한다.

  
<br/>
<br/>

## HTML tag
- **html tag**란 파일의 **content**의 구성을 나타내는 것으로, **어디부터 어디까지**가 title이고 무엇이 링크인지 등을 알려주기 위한 수단이다.
- 모든 태그를 다 외우는 것이 아님!! ~~우리에겐 구글링이 있다~~
- **<>: 열림,  </>: 닫힘**  여는 태그와 닫는 태그 사이에 실제로 화면에 보여질 content를 입력한다

- 대표적인 태그 6가지
    1. **div** → 영역을 나눠준다. (ex 문장 줄바꿈)
    2. **p** → 문단(paragraph)을 나눠준다. (<div>보다 줄간격이 큼, 긴 텍스트를 위한 태그)
    3. **img** → 이미지를 넣어준다. 
        
       - 여는 태그/닫는 태그가 따로 나눠져 있지 않음(self-closing tag)
        
       - 속성값 **src**(source) = 이미지 파일 링크(주소) or 로컬 파일 경로(절대/상대)
        
    4. **input** → 검색창과 같이 무언가를 입력하는 칸을 만든다.(self-closing tag)
        
       - 속성값 **type** = 입력 받는 값의 속성을 지정해 줌(text, number, password, ...) 
        
    5. **button** → 누를 수 있는 버튼을 만든다. (input의 type="submit"과 유사함)
    6. **a** → 다른 웹사이트로 이동할 수 있는 하이퍼 링크를 만들어준다. (anchor)
        
       - 속성값 **href** (HTTP reference or hyperlink reference)= 이동할 주소값 입력
        
       - **target** = “_self” → 같은 탭에서 열림(돌아오기 가능)/ “_blank” → 다른 탭에서 열림 
        
    <br/>
  
    - **Attributes**(속성값)
        - 태그에 추가 정보를 제공,  open tag 안에 큰따옴표와 함께 작성 (with space!!!)
        - 여러 태그에서 공통으로 사용하는 attribute도 존재함
        
    - **self-closing tag**
        - 여는 태그, 닫는 태그가 따로 존재하지 않는다.
        - content가 따로 주어지지 않고, attribute로 모든 정보를 제공 받는 태그이다.
   
 
<br/>

### More HTML tags
      
[HTML elements reference - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

   
<br/>
<br/>
  
## Form Tags
- form = 데이터를 수집하는 컨트롤러
- form 태그 생성 → 이 태그 안에 모든 form tags를 작성함!!
- form 양식
    - input
        - type=”text / color / password / number / file / ... ”
        - input의 type에 따라 적용 가능한 attributes도 달라짐
        - type=”submit”인 경우 button 만들기 가능(form을 어디론가 보내는 것- refresh)
        - placeholder=”입력할 내용 안내”
        - value=”submit button의 이름 바꾸기”
    - label
        - form에 (question + 체크박스)를 추가
        - input 태그와 함께 사용해야 작동한다! (label이 input을 활성화시킴)
        - <label> 태그에 **for=””** 속성값 넣고 <input/> 태그에 **id=””** 속성값 넣기
        - **for과 id에 들어가는 값은 동일해야 한다**! (짝꿍)
        - label 태그의 for과 같은 값을 가지고 있는 id를 찾아서 input을 작동 시킴

<br/>
<br/>    

## **id** = unique identifier (**고유 식별자**)
- **어떤 태그에도 사용 가능**한 attribute
- **element(태그) 당 하나의 id**만을 가질 수 있고, 다른 id 값과 **중복은 허용되지 않는다**.
- 각 태그의 id가 고유한 값을 가지기 때문에 CSS가 **각각의 content를 구분**하여 디자인할 수 있다!

<br/>
<br/>

## Semantic HTML
- semantic하다 = 문서를 보기만 해도 그 의미를 짐작할 수 있는 것
- non-semantic tags: 기능은 존재하지만 문서 내에서 큰 의미가 없는 태그 (generic)
    - div: 영역을 나눠줌 (division). id 속성값을 통해서 의미를 가질 수 있다.
    - span:  짧은 text를 위한 태그
    - 이러한 태그를 무분별하게 사용하면 코드 자체가 복잡해지고 이해하기 번거로워진다.
- **semantic tags**: 의미와 역할을 직관적으로 이해할 수 있는 태그
    - header: div와 같은 기능을 하지만 보자마자 해당 content가 website의 header임을 바로 알 수 있음
    - main: 메인 본문
    - aside/sidebar: main에는 포함되지 않는 content
    - footer : 꼬리말 (&copy;)
    
    - 다른 semantic tags ⇒ mdn → **Content sectioning** 참조
 
 - semantic tags를 활용해서 브라우저와 사용자가 이해하기 쉽도록 **코드를 명확하게** 짜는 것이 중요하다!
