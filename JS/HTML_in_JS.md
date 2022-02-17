## JS & HTML

자바스크립트는 HTML과 상호작용을 하기 위해 사용한다.

JS 파일을 통해서 서버와 클라이언트 간의 communication이 이루어지기 때문에, JS를 통해서 요소들을 다루는 법을 확실하게 익힐 필요가 있다.

즉, HTML의 요소들을 자바스크립트를 통해 접근하고 읽어와서 변경할 수 있어야 한다!

<br/>

### document

JS 콘솔에서 **HTML 문서**를 확인할 수 있는 브라우저의 핵심 객체(object)

콘솔에 document를 입력하면 JS와 연결된 HTML 요소들을 가져와서 **객체로(JS의 관점에서)** 보여준다.

document의 속성에는 HTML 파일에 접근할 수 있는 수많은 옵션들 존재한다! 

ex) document.title = html의 head에서 설정한 웹사이트의 title

<br/>

### JS에서 HTML 요소 가져오기(grab)

1. **태그 이름**으로 불러오기
    
    **document.getElementsByTagName(”tagName”)** ⇒ 해당 html 태그를 반환해주는 함수
    
    한 종류의 태그가 여러 개 존재할 수 있기 때문에 array를 반환한다. 
    
2. **id**로 불러오기
    
    **document.getElementById(”id”)** ⇒ 해당 id를 갖는 하나의 html 태그를 반환해주는 함수
    
3. **class**로 불러오기
    
    **document.getElementsByClassName(”className”)** ⇒ 해당 class를 갖는 html 태그를 반환해주는 함수
    
    같은 class를 갖는 태그가 여러 개 존재할 수 있기 때문에 array를 반환한다.  
    
4. **이름**으로 불러오기
    
    **document.getElementsByName(”Name”)** ⇒ 해당 html 태그를 array로 반환해주는 함수
    
5. **document.querySelector(”조건”) ❤**
    
    조건에 맞는 하나의 HTML 요소를 CSS selector 방식으로  반환하는 함수(#id, .class ...)
    
6. **document.querySelectorAll(”조건”)**
    
    CSS selector의 방식으로 조건에 맞는 모든 HTML 요소를 array로 반환하는 함수
    

💥 HTML의 **head, body, title**과 같이 중요한 요소들은 **document.element**의 형식으로 바로 불러올 수 있지만, 나머지 태그들은 위와 같은 방식으로 호출해야 한다.
