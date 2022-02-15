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

<br/>

### Events

- event = 사용자가 브라우저 내에서 어떤 행위를 하는 것. (click, copy, paste, press Enter, ...)
    
    JS는 브라우저에서 일어나는 모든 event를 듣고 알아차릴 수 있다.
    
- HTML element를 console.dir()를 통해 살펴보면, JS objects 중 이름 앞에 **on**이 붙은 것들은 모두 해당 element가 listen할 수 있는 events에 속한다. (onclick, onchange, onclose, ...)
    
    실제 property는 앞의 on을 제거한 뒷부분에 해당한다. (click, change, close, ...)
    
- event에 대한 정보 → HTML element - Web APIs MDN 찾아볼 것 (JS 관점의 HTML element 정보 페이지)

- JS에서 event를 처리하는 방법
1. **eventListener** = JS에게 무슨 event를 듣게 하고 싶은 지를 알려주는 작업
    
    ```jsx
    htmlElement.addEventListener("event", functionName);
    
    // 예시
    const title = document.querySelector("h1");
    title.addEventListener("click"); // 사용자가 title을 클릭하는 이벤트를 listen해라
    
    /* click event가 발생했을 경우 무언가 변화를 주고 싶다면 
    -> eventListener에 함수를 넘겨주면 된다.*/
    
    function handleTitleClick() {
    	console.log("title was clicked!");
    }
    title.addEventListener("click", handleTitleClick);
    /* 이때 함수를 코드 내에서 실행시키지 않고 JS에게 function 이름을 넘겨주기만 함으로써
    해당 이벤트가 발생했을 때 JS가 알아서 함수를 실행시키도록 해야 한다.*/
    ```
    

1. **on*event***
    
    ```jsx
    htmlElement.onevent = functionName;
    
    // 예시
    const title = document.querySelector("h1");
    
    function handleTitleClick() {
    	console.log("title was clicked!");
    }
    
    // on*event*는 function이 아니기 때문에 onevent() 식으로 작성하지 않는다.
    title.onclick = handleTitleClick;
    ```
    

💥 두 가지 방법은 모두 동일하지만, 첫 번째 방법의 경우 **removeEventListener**를 통해서 추가된 event listener를 제거할 수 있다.

<br/>

### Window Events

JS에서 기본 제공되는 window 객체를 통해 윈도우에서 발생하는 event도 감지할 수 있다.

```jsx
function handleWindowResize() {
	document.body.style.backgroundColor = "tomato";
}

//window element에서 크기 변경 이벤트가 발생할 경우 해당 함수를 실행
window.addEventListener("resize", handleWindowResize);
```
