# Events

- event = 사용자가 브라우저 내에서 어떤 행위를 하는 것. (click, copy, paste, press Enter, ...)
    
    JS는 브라우저에서 일어나는 모든 event를 듣고 알아차릴 수 있다.
    
- HTML element를 console.dir()를 통해 살펴보면, JS objects 중 이름 앞에 **on**이 붙은 것들은 모두 해당 element가 listen할 수 있는 events에 속한다. (onclick, onchange, onclose, ...)
    
    실제 property는 앞의 on을 제거한 뒷부분에 해당한다. (click, change, close, ...)
    
- event에 대한 정보 → HTML element - Web APIs MDN 찾아볼 것 (JS 관점의 HTML element 정보 페이지)

<br/>


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

<br/>

### 입력값(value) 받아오기

HTML의 input을 이용해서 입력 받은 값을 변수에 저장하기 ⇒ input.**vaule 속성**

```jsx
const loginForm = document.getElementById("login-form");
const loginInput = loginForm.querySelector("input");
const loginButton = loginForm.querySelector("button");

function onLoginClick() {
  const username = loginInput.value;
  console.log(username);
}

// click event가 발생하면 input의 value를 console.log한다.
loginButton.addEventListener("click", onLoginClick);
```

<br/>

### Form Submission

HTML의 form의 기능을 활용하면, JS에서 굳이 click event를 listen하지 않아도 입력 받은 정보를 다른 곳으로 submit하는 것이 가능하다. (just Press Enter or Click the btn in the form)

하지만, form이 submit됨과 동시에 웹페이지 전체가 새로 고침 되는데, 이때  input의 value를 가져오기 위해서는 웹페이지가 새로 고침 되는 것(form의 submit event)을 막아주는 작업이 필요하다. (새로 고침 되어버리면 입력 값을 저장해도 날라가기 때문)

<aside>
💡 중요한 건 input/button을 click하는 event가 아닌 **form 그 자체의 submit event!**

</aside>

```jsx
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");

function onLoginSubmit() {
  const username = loginInput.value;
  console.log(username);
}

// form 자체에서 submit event가 발생하면 input의 value를 console.log한다.
loginForm.addEventListener("submit", onLoginSubmit);
```

- submit event를 감지해서 value를 console.log할 수 있다.
- 하지만, form이 submit됨과 동시에 웹페이지 전체가 새로 고침(form submit의 기본 동작) 되는데, 이때  input의 value를 가져오기 위해서는 브라우저가 새로 고침 되는 것을 막아주는 작업이 필요하다. (새로 고침 되어버리면 입력 값을 저장해도 날라가기 때문)

💥 firstArgument.**preventDefault()** ⇒ eventListener의 첫 번째 argument 안에 존재하는 함수로, 브라우저가 **event의 기본 동작을 실행하지 못하게 막아준다.**

<br/>

### Event Function

앞서 살펴본 eventListener는 특정 이벤트가 발생했을 때, 입력 받은 이름의 함수를 실행시키는 역할을 한다. 이때 eventListener를 통해 실행되는 함수는 그 **첫 번째 인자**로 방금 발생한 **이벤트의 정보**를 담아서 호출된다. (ex 무엇이 클릭 되었는지, 어디가 클릭 되었는지 등)

💥 JS가 이벤트에 대한 정보를 받아오기를 원한다면, 함수 선언 시 **정보를 받아 올 공간을 제공**해주어야 한다. (function에 argument 주기, 일반적으로 인자명을 **event**로 설정한다.→ event 객체의 정보를 받아온다는 의미)

💥 그렇게 받아 온 첫 번째 인자(변수)에 대하여 **preventDefault()** 함수를 실행해주면 브라우저가 새로 고침 되는 것을 막으면서 event 정보를 받아올 수 있다.

💥 이벤트에 대한 옵션 정보가 필요하지 않은 작업의 경우, 굳이 인자를 받아올 필요는 없다.

```jsx
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");

function onLoginSubmit(event) {
	event.preventDefault(); // submit 이벤트로 인한 새로고침 방지
	//console.log(event); // 발생한 이벤트에 대한 정보 출력
  console.log(loginInput.value); // 입력값 출력
}

// form 자체에서 submit event가 발생하면 input의 value를 console.log한다.
loginForm.addEventListener("submit", onLoginSubmit);
```
