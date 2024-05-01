ctrl + alt + f11 라이브코드 컴파일 단축키  
F11(몰입모드) -> 삼선 -> 캡쳐
가끔은 껏다키면 해결 되는게 있다...  
Shift + 1~4 모드선택 단축키  
우클릭 + c 확대 +z 축소  
## 만약 에디터가 이전 변경사항이 적용 안되어있다면 에디터를 닫고 vscode에서 shift+ctrl+b로 다시 돌리고 열면 됌  

![어떻게 돌아가는지](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/b9c39707-07d6-4cf7-81dd-da71b37da42b)  

라이브 코딩은 에디터를 껏다가 키면 초기화 되기때문에 에디터를 키기전에 vscode에서 crlt shift b 로 빌드작업 하고 에디터를 닫아놓은체로 전체를 컴파일해야함  

<details>
<summary><p>$\huge{\rm{\color{#6580DD}ERROR LIST}}$</p> </summary>


### 1.캐릭터가 움직이지를 않음 
해결: 게임 모드 설정과 껏다 켰다를 하니 해결됨
### 2.게임 시작시 프리징  
이유: tick코드안에 바로 반복문써서 과부하걸린거임
### 3.github desktop "the remote disconnected. check your internet connection and try again." 
이유: 한번에 푸시하는 양이 많아서 그럼  
### 4.포인터에 null값이 들어갔다
![image](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/7689ee0d-be27-42f2-b502-ab894364a9c1)
### 5. PIE: Error: Blueprint Runtime Error: "Accessed None trying to read property Grabber". Node:  Release Graph:  EventGraph Function:  Execute Ubergraph BP First Person Character Blueprint:  BP_FirstPersonCharacter  
이유: Grabber'라는 속성에 접근하려 했으나 그 객체가 존재하지 않을 때 발생 
해결: 삭제하고다시 추가해주니 해결되었다. 
</details>


<details>
<summary><p>$\huge{\rm{\color{#6580DD}C++}}$</p></p> </summary>

### FCollisionShape Sphere = FCollisionShape::MakeSphere(GrabRadius);
FHitResult HitResult;

### UPROPERTY
변수위에 UPROPERTY()를 작성  
EditAnywhere을 괄호안에 넣으면 어디서든 에디터에서 값을 변경할 수 있다는것  
헤더파일에 작성했던 그 변수들이 객체의 디테일에 담겨서 나옴  

### UFUNCTION
함수위에 UFUNCTION()은 함수를 보이게하는 것
BlueprintCallable 블루프린트에서 엑세스 할 수 있게 해줌
이때 에디터와 라이브 코드를 끄고 vscode에서 별도로 빌드를 돌린후 파일에 들어가서 켜야함  

### TYPE
int32는 32비트인 정수를 나타낸것이다
FVector는  벡터를 선언할때
FString은 문자열을 선언할때

<details>
<summary><p>$\huge{\rm{\color{#6580DD}ABOUT FUNCTION}}$</p></p> </summary>

## GetSafeNormal()
주어진 벡터를 그 크기로 나누어 단위 벡터를 생성

## GetOwner()
오너 포인터를 가져와주는 함수
해당 Component를 소유한 Actor의 주소를 저장할때 사용함
Component를 통해 Actor에게 사운드를 부여하거나 Actor의 위치를 파악하거나 설정하는 등의 작업을 수행하려면 포인터를 액터에 전달해야 함

## FVector::Distance(a,b)
a와 b 사이의 거리를 구해준

## Tick()
매프레임마다 안에 있는 코드들을 호출해줌  
올바르게 반복문을 만들었어도 tick함수 내에서 만든거라면 프리징 현상이 일어날 수 있으니 사용할때 극.구.조.심  
매프레임 log를 찍는것은 오류가 안남  

<details>
<summary>Trace </summary>

### 라인트레이스 
섬세하게 탐지할때 주로 사용
선으로 탐지  
FPS게임이나 오브젝트를 잡을때  

### 셰이프 트레이스(지오메트리 트레이)  
도형으로 탐지  

### 트레이스 채널
트레이스에 반응할 수 있는 목록만 생성하고 나머지는 무시

### 비지빌리티 트레이스 채널
눈에 보이는 모든 오브젝트

### 카메라 트레이스 채널
이 오브젝트를 투시하도록 허용할지

</details>

### Extra
일반적으로 포인터가 있는 경우 화살표 연산자(->)  
FString FVector와 같은 구조체가 있는 경우 점 연산자(.) 사용  

</details>


## 클래스 자체에서 함수를 가져올때 ::를 사용

## HitResult
HitResult.Location 객체 중심으로의 1미터 반경의 구체를 건듦  
HitResult.ImpactLocation 객체의 표면을 건듦

### UPROPERTY
UPROPERTY(EditAnywhere)은 어디서든 볼수있고 편집할수이다는 것
UPROPERTY(VisibleAnywhere)은 어디서나 볼수만 있다는 

### DebugDraw
DrawDebugLine(GetWorld(), Start, End, FColor::Red);
시작점,끝점,색깔  
DrawDebugSphere(GetWorld(), End, 10, 10, FColor::Blue,true, 5);
구체의 중심, 반경, 조각갯수, 색깔, 지속방식(true = 한번만 호출, 지속시간 무), 지속시

### const(안정성 증가)
값이 변하지 않는것에 사용함
사용가능 여부는 마우스를 가져다두고 뜨는 창을보고 알수도 있다. 

### 로그
로그를 찍을때 string은 *를 붙어야지 사용 가능하다
display warning Error로 색깔을 다르게하여 경고와 에러를 잘보이게 할수있음
ex) UE_LOG(LogTemp, Display, TEXT("Here's My String: %s  %f"),*MyString, MoveDistance);

## 컴포넌트에 접근
UPhysicsHandleComponent* PhysicsHandle = GetOwner() -> FindComponentByClass<UPhysicsHandleComponent>();
컴포넌트에서 physicshandle컴포넌트에 접근하게하는 코드
</details>

<details>
<summary><p>$\huge{\rm{\color{#6580DD}BLUE PRINT}}$</p></p> </summary>

BP는 블루프린트 클래스라는 뜻  
발사체를 주로 ProjectTile이라고 부름  
맵마다 각자의 블루 프린트가 있음  

## In BluePrintEditor
1. create reference는 그 물체의 주소를 저장하는거임
2. 파란색 핀은 실행 핀(excution pin)임
3. space bar를 검색하면 space bar입력노드가 생김 add impulse와 연결하면 space bar누를 시에 어느 방향으로 이동할지 정할수있음(질량*100부터 약간의 효과가 보임)
4. add impulse에 있는 vel change는 체크하면 질량을 무시하고 속력을 정할 수 있게해줌
5. impulse에 직접 연결하면 기본단위가 cm이기에 1cm임
6. muliply를 통해서 값을 조절한 후에 impulse에 연결하면 된다
7. get변수를 만들고 subtract로 원하는 만큼 값을 빼고 다시 set변수로 값을 계속 변화 시키고 저장할 수 있다.

### SideEffect(함수가 실행되고 식별 가능한 효과가 생기는거)
EX) print string, add, impulse set 같은거

### 순수함수(SideEffect가 없는)
디테일에서 퓨어를 눌러 함수를 순수함수(SideEffect가 없는)로 바꿀수 있다. (간단한 코드에서 사용) 
EX) 실행핀이 없는 Get, Get Actor Forward Vector, Multiply,Minus,Greater수학함수 같은 것들

암묵적으로 모든 멤버 함수는 현재 타겟이나 현재 인스턴스라는 파라미터를 가지고 있다  
Project Tile 자체에서 만든 함수를 map의 BluePrint에서 실행 핀을 통하여 연결할 수 있다. (멤버 함수의 개념)  
트랜스폼의 자물쇠를 누르면 값을 다같이 바꾸는걸로 설정할 수 있다.  

플레이어 물리충돌을 처리하기위해 charactor movmnet로부터 두개의 moveupdatecomponent로 충돌 처리 그리고 캐릭터의 회전을 위해 get actor rotation을 만듦  


</details>


------------------------------------------------------------------

에셋은 maps에서 작성자가 미리보기 느낌으로 만든곳에서 미리 볼수있다.
mesh에서 꺼내쓸수 있따.

brush로 생성된 물체는 크기 설정은 scale보다 브러시 세팅으로 하는게 좋다

mesh를 다른 mesh의 디테일에다가 끌어놓아서 자식으로 만들어 종속 시킬수있

mesh를 더블 클릭하여 편집에 들어간후 콜리전을 삭제 시킬수도있다.

미리보기 모드에서 오른쪽 상단에 격자무늬 아이콘을 누르면 4분할로된 각 방명에서의 맵의 구성을 볼수있다

Actor Component
모든 액터에 접근되는 기본적인 Component 이다

Scene Component
Transform이 있는 Actor Component이고 다른 Scene Component에도 접근할 수 있다
서로 접근이 가능하다면 디테일에 같은 섹션에 있다.

------------------------------------------------------------------------

<details>
<summary><p>$\huge{\rm{\color{#6580DD}Unreal Editor}}$</p></p> </summary>

<details>
<summary><p>$\huge{LandScpae Mode}$</p> </summary>

## Number of Components
땅 크기 조절  

## Pint
레이어의 +표시 눌러서 weightlender로 서로 겹칠때 혼합되게 할지 Non weightblender로 그위에 그냥 쌓이게 할지 정할수 있음  

<details>
<summary><p>$\huge{Light}$</p> </summary>

## static
게임에서 빛에 관련된걸 바꿀수 없게함(성능향상에 도움)  

## Stationay
빛의 색과 강도 조절가능  
위치와 회전은 불가능  

## Movable
움직이는 태양과 그림자 나타낼  

### pointlight 
그냥 한점에서 빛이 밖으로 나감 광원이 하나라는게 핵심  

### SpotLight
빛의 방향이 하나임 특정 영역이나 객체를 비출때 용이  

### RectLight
빛이 한면 전체에서 나옴 넓은곳을 비출때 용이  

### Directional Light 
태양을 추가한다고 생각하면 편함  
skysphere안의 detail에 들어가서 서로 연결해주면 각도에 다른 하늘 변화를 만들수있음   
ctrl + L로 태양위치 시각적으로 더 잘보이게 바꿀수있음  

### SkyLight
레벨에서 멀리 떨어진 빛을 캡쳐해서 씬에 적용 우리 레벨 전체를 감싸는 구를 추가한다고 생각하면 됌 하늘같은 거    
이때 사용할 메시를 찾을려면 (콘텐츠 드로어 -> show engine content -> engine파일 -> sky)  
씬 recapture라는 속성에 recapture를 누르면 씬의 조명이 업데이트됨  

Tempeture로 태양의 색깔을 바꿀 수 있음  

### Sky Atmosphere
지구 같은 대기 생성
다른 광원을 하나 더 만들수 있음(달 또는 두 번째 태양 생성)

조명BP를 사용할때 그 객체의 light에 들어가서 값을 설정할 수 있다.
intensity는 밝기 조절
attenuation 반경 설정(설정해서 성능에 도움을 줄수있음)


</details>

<details>
<summary><p>$\huge{Meterial}$</p> </summary>

## 설정
Fully rough는 무광으로 설정하게 하는거  
Layers를 추가해서 Layer Blend노드에 이름을 달아 줄수 있다.  

### Layers의 Blender Type
Weight Blender 이 meterial layer를 다른 meterial레이어와 블렌딩할 수 있게함   

## Extra
meterial뒤에 있는 inst 진짜 메테리얼이 아니라는 뜻임  
우클릭 -> 부모찾기 -> master이라는 이름이 붙은 메테리얼이 나옴 이게 진짜 머티리얼을 만드는거  

detail의 mobility에 
static으로 게임 시작전에 미리 조명 설정과 같은 작업을 마칠수있다
Stationary로 객체를움직일 수는 없지만 밝기 같은 건 바꿀수 있다. 
Movealbe로 모든 걸 변경할수있게 할수있다.




### 루멘은 Moveable로 가장 잘 돌아간다

바닥이 있지만 떨어질때는 객체의 에디터를 켜서 왼쪽위 콜리전에서 시각화를 작동시키고 디테일에서 collison에서 z축 설정해준다 -10정도





## Udemy Edition
Inheritance(상속)
하위 클래스가 상위 클래스의 모든 기능을 자동적으로 물려받는 것
![예시](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/598176a6-c97a-481e-b9e9-d5899d34ef18)



Composiotion
클래스 A가 클래스B의 인스턴스를 포함한다고 말할 수 있고 해당 기능을 사용할 수 있지만 클래스 B에 소속된 것이 아니라 원하는 부분만 선택해서 가져갈 수 있다 클래스 A가 클래스 B를 포함하는 것
![예시](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/6a999470-c8e1-4202-8c58-134671232b79)

![예시](https://github.com/REWELLGOM/Learn-Unreal/assets/129605750/1c6e35c5-797e-4399-9464-fe5577a7b2d8)

</details>

