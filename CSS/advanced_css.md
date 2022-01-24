# Advanced CSS


### Transition
- 어떤 상태에서 다른 상태(state)로의 **변화**를 보여주는 애니메이션
- state가 없는 element과 state가 있을 때의 스타일(active, hover...)이 설정되어 있을 때, **state가 없는 요소(root)에 사용**하여 non-state → state까지의 과정에 **효과**를 주는 속성
- **transition: 변화할 속성  변화 시간  변화 양상(ease-in-function);**
- transition에서 변화할 부분은 state가 있을 때의 스타일 내에 존재해야 한다.
    
    (여러 속성을 설정하고 싶다면 콤마로 구분하여 각각 작성, 모든 속성을 선택하고 싶다면 **all**을 작성, 일부만 다르게 하고 싶다면 all 설정 뒤에 따로 추가)
    
- **ease-in function**
    - 브라우저에게 애니메이션이 어떻게 변할 지를 말해줌
    - linear : 같은 속도로 직선으로 이동
    - ease-in :  끝에서 빨라짐
    - ease-out : 끝에서 느려짐
    - ease-in-out : 느리게 시작했다가 빨라지고 끝에서 다시 느려짐
    - cubic-bezier: 사용자 정의 애니메이션 (가속, 감속 정도를 설정 가능)
    
    [Ceaser CSS Easing Animation Tool](https://matthewlein.com/tools/ceaser)
    
<br/>
<br/>

### Transformation
- 원하는 요소를 변형시킬 수 있다. (3D 회전, 크기 변경, 기울이기, 위치 이동, ...)
- **transform: 명령어(value);**
- 다른 box 요소를 변형시키지 않는다!
- box 차원에서 일어나는 변화가 아니기 때문에 옆의 sibling들에게 영향을 끼치지 않는다.
    
    (이동하면 옆에 있는 요소가 밀리는 게 아니라 겹쳐서 나타나고, margin, padding이 적용되지 않는다.)
    
- transition과 transformation은 결합이 가능하다!
    - state가 있을 때의 스타일에 transformation을 설정해주면 요소 변형이 상태에 적용됨!

  [transform - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/ko/docs/Web/CSS/transform)
