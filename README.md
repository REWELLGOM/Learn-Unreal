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

에셋은 maps에서 작성자가 미리보기 느낌으로 만든곳에서 미리 볼수있다.
메쉬에서 꺼내쓸수 있따.

브러시로 생성된 물체는 크기 설정은 scale보다 브러시 세팅으로 하는게 좋다
