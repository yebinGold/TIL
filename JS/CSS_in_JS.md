## JS & CSS

JS에서도 element의 style을 설정하고 변경할 수 있지만, style 설정의 경우 CSS 파일에서 이루어지는 것이 바람직하다.

### classList

- CSS에서 설정한 class 속성을 JS를 통해 HTML에 적용 시킬 수 있다.
- 기초적인 방법으로, JS에서 불러온 HTML 요소의 className을 변경해줄 수 있지만, 이는 하나의 요소에 할당된 클래스가 여러 개인 경우 고려해야 할 사항이 복잡해질 수 있다.
- HTML 요소가 가진 class를 하나의 배열로 다루는 classList의 함수들을 이용하면 훨씬 쉽게 작업할 수 있다.

- element.**classList.add**(className) : 해당 클래스 추가
- element.**classList.remove**(className) : 해당 클래스 제거
- element.**classList.contains**(className) : 해당 클래스 포함 여부를 boolean값으로 반환

### toggle

- list.toggle(token)
- 주어진 리스트 안에 token이 존재한다면, 이를 제거하고 없다면 추가하는 함수
- if-else문을 효과적으로 대체할 수 있다.
```javascript
// css로 작업 넘기기
// css에서 미리 active라는 이름의 class를 정의해놓고 JS에서 사용한다.

function handleTitleClick() {
  /*
  const clickedClass = "active";
  if (title.classList.contains(clickedClass)) {
    title.classList.remove(clickedClass); // class 없애주기
  } else {
    title.classList.add(clickedClass); // css에서 저장한 클래스 이름을 html에 할당
  }*/
  title.classList.toggle("active");
}

title.addEventListener("click", handleTitleClick);
```
