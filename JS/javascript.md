# JavaScript
웹사이트의 interactivity를 담당하는 언어. <br/>
모든 브라우저 내에 존재하기 때문에 따로 다운로드할 필요 없이 브라우저의 콘솔 창에서 접근할 수 있다.
하지만 콘솔은 긴 코드를 작성하는 용도가 아니기 때문에, IDE에서 *.js 파일을 생성하여 사용한다.

<br/>

## JS에서의 변수(variable) 선언

1. **const** 키워드(상수, constant)를 사용하여 변수를 선언한다.

      ```const var_name = value;```

    - 재선언, 재할당을 할 수 없다! (같은 변수 이름으로 재선언 불가, 초기값 수정 불가)

2. **let** 키워드를 사용하여 변수를 선언한다.

    ```let var_name = value;```

    - 재선언 불가, 재할당은 가능

3. **var** 키워드를 사용하여 변수를 선언한다.

    ```var var_name = value;```

    - 재선언, 재할당 모두 가능
    - 초기 JS에서의 변수 선언 방식. 실수로 값을 업데이트 해도 문제를 알 수 없다는 단점이 있다.
    - 이후 언어 차원에서 변수 값의 보호를 위해 const(수정 불가)와 let(수정 허용)이 등장했다.

💥 변수 이름을 설정할 때 띄어쓰기(snake_case)를 사용하지 않고, 보통 대문자로 표현한다(**camelCase**)  
    ex) my_variable (X) myVariable (O)

💥 변수를 선언할 때 바로 초기값을 할당할 수 있고, undefined 상태로 둘 수도 있다.

💥 기본적으로 const를 사용하되, 값의 업데이트가 필요한 경우라면 let을 사용한다.

💥 var의 경우, 사용에 문제는 없지만 값의 수정 가능 여부에 대한 정보를 담지 못하기 때문에 권장되지 않는다.

<br/>

### Array(배열)

변수에 여러 값을 할당하고 싶을 경우 사용하는 데이터 구조.

파이썬과 같이 대괄호[ ] 안에 값들을 입력하고, 인덱스로 항목에 접근할 수 있다.

```jsx
const day = ["mon", "Tue", "Wed", "Tur", "Fri", "Sat"];

// 새 항목 추가
day.push("Sun");

// 인덱스로 접근
console.log(day[1]);
```

- array 내장 메소드
    - arr.push(elem) ⇒ 배열 arr에 elem을 추가하는 함수
    - arr.indexOf(elem) ⇒ elem이 몇 번째 인덱스인지 알려주는 함수
    - arr.splice(start, n) ⇒ 배열의 start 인덱스부터 n개의 항목을 제거하는 함수
    - arr.slice(start, end) ⇒ 배열의 start부터 end-1 인덱스까지의 항목을 슬라이싱 하는 함수. 기존의 오리지널 데이터(arr)에는 영향을 미치지 않는다.
    - arr.map(조건)  ⇒ 배열 내 각각의 항목들을 조건에 맞게 변환하여 새로운 배열에 저장하는 함수
    - arr.sort() ⇒ 배열 내 항목들을 정렬하는 함수. 오리지널 데이터를 변환한다.
    - arr.filter(조건) ⇒ 조건을 만족하는 값들만 추출하여 새로운 배열에 저장하는 함수

💥 const로 배열을 선언할 경우, 변수 자체는 재할당이 불가능하지만 배열 내 항목들은 추가, 삭제가 가능하다.

💥 하나의 배열에는 공통의 속성을 가진 데이터들만 저장한다.

<br/>

### Object(객체)

property(속성)를 갖는 데이터를 저장하는 구조. 

array가 같은 속성을 갖는 데이터들을 나열하는 구조라면, object는 서로 다른 속성들을 하나의 그룹으로 묶어서 정리한다. 

배열 선언과 유사하지만, 중괄호{ } 를 사용하여 선언한다.

```jsx
const object = {
	prop1: value1;,
	prop2: value2;
}

// 예시
const player = {
	name: "mango",
	points: 10,
	life: 3
};

// 객체를 통째로 불러오기
console.log(player);

// 객체의 각 속성들만 불러오기 (각각 접근 가능)
console.log(player.name); // 접근 방법 1
console.log(player["name"]); // 접근 방법 2

// 객체 내 속성값 변경하기
player.points = 50; // 기존 속성의 value를 재할당(업데이트)

// 객체에 속성 추가하기
player.damage = 15; // 새로운 속성 damage 추가
```

💥 객체의 property-value 관계는 파이썬 딕셔너리의 key-value 관계와 유사하다.

💥 객체 내 property를 수정하는 것은 가능하지만, 이미 선언된 object 자체를 변경할 수는 없다.
