# Learn-Unreal

## 가끔은 껏다키면 해결 되는게 있다...


### 블루프린트
블루프린트에 create reference는 그 물체의 주소를 저장하는거임
파란색 핀은 실행 핀(excution pin)임

space bar를 검색하면 space bar입력노드가 생김 
이거를 add impulse와 연결하면 space bar누를 시에 어느 방향으로 이동할지 정할수있음
(질량*100부터 약간의 효과가 보임)
add impulse에 있는 vel change는 체크하면 질량을 무시하고 속력을 정할 수 있게해줌

BP는 블루프린트 클래스라는 뜻
발사체를 주로 ProjectTile이라고 부름

impulse에 직접 연결하면 기본단위가 cm이기에 1cm임
muliply를 통해서 값을 조절한 후에 impulse에 연결하면 된다

맴마다 각자의 블루 프린트가 있다.

get변수를 만들고 subtract로 원하는 만큼 값을 빼고 다시 set변수로 값을 계속 변화 시키고 저장할 수 있다.


### SideEffect(함수가 실행되고 식별 가능한 효과가 생기는거)
EX) print string, add, impulse set 같은거

### 순수함수(SideEffect가 없는)
디테일에서 퓨어를 눌러 함수를 순수함수(SideEffect가 없는)로 바꿀수 있다. (간단한 코드에서 사용) 
EX) 실행핀이 없는 Get, Get Actor Forward Vector, Multiply,Minus,Greater수학함수 같은 것들

------------------------------------------------------------------

에셋은 maps에서 작성자가 미리보기 느낌으로 만든곳에서 미리 볼수있다.
mesh에서 꺼내쓸수 있따.

brush로 생성된 물체는 크기 설정은 scale보다 브러시 세팅으로 하는게 좋다

mesh를 다른 mesh의 디테일에다가 끌어놓아서 자식으로 만들어 종속 시킬수있

mesh를 더블 클릭하여 편집에 들어간후 콜리전을 삭제 시킬수도있다.
