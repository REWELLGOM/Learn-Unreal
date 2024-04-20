# Learn-Unreal

가끔은 껏다키면 해결 되는게 있다...

# C++
블루포인트에 표시하게하는 방법으로 변수위에 UPROPERTY(EditAnywhere)를 작성
헤더파일에 작성했던 그 변수들이 객체의 디테일에 담겨서 나옴

int32는 32비트인 정수를 나타낸것이다

Tick 함수 매프레임마다 호출해줌
올바르게 반복문을 만들었어도 tick함수 내에서 만든거라면 프리징 현상이 일어날 수 있으니 사용할때 극.구.조.심
매프레임 log를 찍는다고해서 오류는 안남

Pseudocode(의사 코드): 알고리즘단계에서 일반적인 언어로 설명한것
### 선언
FVector는  벡터를 선언할때
FString은 문자열을 선언할때

코드 작성전에 주석으로 미리 어떤걸 구현해야할지 써놓는게 좋다

GetSafeNormal()
주어진 벡터를 그 크기로 나누어 단위 벡터를 생성

클래스 자체에서 함수를 가져올때 ::를 사
UPROPERTY(EditAnywhere)은 어디서든 볼수있고 편집할수이다는 것
UPROPERTY(VisibleAnywhere)은 어디서나 볼수만 있다는 

### 로그
로그를 찍을때 string은 *를 붙어야지 사용 가능하다
display warning Error로 색깔을 다르게하여 경고와 에러를 잘보이게 할수있음
ex) UE_LOG(LogTemp, Display, TEXT("Here's My String: %s  %f"),*MyString, MoveDistance);

## 만약 에디터가 이전 변경사항이 적용 안되어있다면 에디터를 닫고 vscode에서 shift+ctrl+b로 다시 돌리고 열면 됌
![어떻게 돌아가는지](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/b9c39707-07d6-4cf7-81dd-da71b37da42b)


## 블루프린트
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

맵마다 각자의 블루 프린트가 있다.

get변수를 만들고 subtract로 원하는 만큼 값을 빼고 다시 set변수로 값을 계속 변화 시키고 저장할 수 있다.


### SideEffect(함수가 실행되고 식별 가능한 효과가 생기는거)
EX) print string, add, impulse set 같은거

### 순수함수(SideEffect가 없는)
디테일에서 퓨어를 눌러 함수를 순수함수(SideEffect가 없는)로 바꿀수 있다. (간단한 코드에서 사용) 
EX) 실행핀이 없는 Get, Get Actor Forward Vector, Multiply,Minus,Greater수학함수 같은 것들

암묵적으로 모든 멤버 함수는 현재 타겟이나 현재 인스턴스라는 파라미터를 가지고 있다

Project Tile 자체에서 만든 함수를 map의 BluePrint에서 실행 핀을 통하여 연결할 수 있다. (멤버 함수의 개념)

트랜스폼의 자물쇠를 누르면 값을 다같이 바꾸는걸로 설정할 수 있다.

플레이어 물리충돌을 처리하기위해 charactor movmnet로부터 두개의 moveupdatecomponent로 충돌 처리 그리고 캐릭터의 회전을 위해 get actor rotation을 만듦

------------------------------------------------------------------

에셋은 maps에서 작성자가 미리보기 느낌으로 만든곳에서 미리 볼수있다.
mesh에서 꺼내쓸수 있따.

brush로 생성된 물체는 크기 설정은 scale보다 브러시 세팅으로 하는게 좋다

mesh를 다른 mesh의 디테일에다가 끌어놓아서 자식으로 만들어 종속 시킬수있

mesh를 더블 클릭하여 편집에 들어간후 콜리전을 삭제 시킬수도있다.
