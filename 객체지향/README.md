# 2021-04-26 객체지향 '진짜' 제대로 알기...

## 객체지향이란?
- OOP(Object-Oriented Programming)
- 컴퓨터 프로그래밍 패러다임 중 하나
- 필요한 데이터를 ***추상화*** 행위를 가진 객체를 만들고, 그 객체들간의 ***상호작용***을 통해 로직 구성을 하는 프로그래밍 방법

## 객체지향 프로그래밍의 장점?
- 코드 재사용 : 3rd party Library, 상속을 통해 확장하여 사용 가능!
- 유지보수 용이 : 수정해야 할 부분이 클래스 내부에 멤버 변수 or 메서드로 있기에 찾기 쉬움
- 대형 프로젝트 적합성 : 클래스단위로 모듈화 시켜서 개발할 수 있으므로 대형 프로젝트처럼 여러명이 개발하기 좋다

## 객체지향 프로그래밍의 단점?
- 처리속도가 상대적으로 느림 : JVM
- 객체가 많으면 용량이 커진다.
- 설계시 많은 시간과 노력 필요

## 객체지향 5가지 키워드
1. 클래스+인스턴스 (객체)
  - 클래스란 어떤 문제를 해결하기 위한 데이터를 만들기 위해 추상화를 거쳐 집단의 속하는 **속성**과 **행위**를 변수와 메서드로 정의
  - 인스턴스(객체)란 클래스에서 정의한 것을 실제로 메모리상에 할당된 것 즉, 프로그램에서 사용되는 데이터
2. 추상화
  - 불필요한 정보를 숨기고 중요한 정보만을 표현함으로써 **공통의 속성이나 기능을 묶어 이름을 붙이는 것**
3. 캡슐화
  - 코드를 재수정 없이 재활용하는 것을 목적
  - 관련된 기능과 특성을 한 곳에 모르고 분류
  - 객체 지향 프로그래밍에서 **기능과 특성의 모음을** ***클래스*** **라는** ***캡슐*** **에 분류해서 넣는것**
4. 상속
  - 부모 클래스의 속성과 기능을 그대로 이어받아 사용할 수 있게하고 일부 변경이 가능
  - 다중상속 불가 , 인터페이스는 다중상속 가능 
5. 다형성
  - 오버라이딩과 오버로딩등, 하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석될 수 있는 것


## SOLID 원칙
- 소프트웨어를 설계함에 있어 이해하기 쉽고, 유연하며, 유지보수가 편하도록 도와주는 5가지 원칙
- 단일책임원칙, 개방폐쇄원칙, 리스코프치환원칙, 인터페이스분리원칙, 의존성역전원칙

## 단일 책임 원칙 ( SRT, Single Responsibility Principle )
- 모든 클래스는 단 한가지의 책임을 부여받아, 수정할 이유가 단 한 가지여야 한다.
- 즉, 클래스에 속해있는 멤버들과 메소드는 모두 공통적으로 하나의 서비스를 위해 필요
- 적용 방법
  - 각 책임을 각각의 개별 클래스로 분할
  - 분할 후에도 비슷한 책임을 갖고 있다면 **부모클래스로 추출** , 필드나 메소드를 옮길 수도 있다.
  - 클래스 이름을 해당 클래스의 책임을 나타낼 수 있도록 작성
- SRT 적용 전
```
class Car{
  private String serialNum;
  private String engine;
  private String color;
  private String model
  public Car(String serialNum, String engine, String color, String model){
    this.serialNum = serialNum;
    this.engine = engine;
    ...
  }
}
```
- SRT 적용 후
```
 class Car{
   private String serialNum;
   private CarSpec spec;
   public Car(String serialNum, CarSpec spec){
     this.serialNum = serialNum;
     this.spec = spec;
   }
 }
 
 class CarSpec{
   private String engine;
   private String color;
   private String model;
   public CarSpec(String engine, String color, String model){
    this.engine = engine;
    this.color = color;
    this.model = model;
   }
 }
```
-> 공통으로 쓸수있는 engine, color, model을 추출하여 CarSpec 클래스를 생성했다.
-> 변경이 발생하더라도 Car 클래스를 수정할 필요가 없다.

## 개방 폐쇄 원칙 ( OCP, Open-Closed Principle )
- 소프트웨어의 구성요소 (컴퍼넌트, 클래스, 모듈, 함수)가 **확장**에 대해 **유연**해야 하지만, **수정**에는 **폐쇄적**이어야 한다.
- 관리와 재사용이 가능한 코드를 만드는 기반
- 개방 폐쇄 원칙 적용에 중요한 매커니즘은 **추상화** , **다형성**
- 변경될 것과, 변경하지 않을 것을 구분하여 인터페이스를 정의하고, 구체적 타입 대신 인터페이스에 의존하도록 코드 작성
- 상속보다는 포함 관계를 활용
- OCP 적용 전
```
 class Car{
   private String serialNum;
   private CarSpec spec;
   public Car(String serialNum, CarSpec spec){
     this.serialNum = serialNum;
     this.spec = spec;
   }
 }
 
 class CarSpec{ ... }
 
 class AirPlane{
   private String serialNum;
   private AirPlaneSpec spec;
   public car(String serialNum, AirPlane spec){
    this.serialNum = serialNum;
    this.spec = spec;
   }
 }
 
 class AirPlaneSpec{ ... }
```
- OCP 적용 후
```
 class Car extends Vehicle{
   private String serialNum;
   private CarSpec spec;
   public Car(String serialNum, CarSpec spec){
     this.serialNum = serialNum;
     this.spec = spec;
   }
 }
 class CarSpec extends VehicleSpec{ ... }
 
 class AirPlane extends Vehicle{ ... }
 class AirPlaneSpec extends VehicleSpec{ ... }
```

## 리스코프 치환 원칙
- 상위 타입은 항상 하위 타입으로 대체할 수 있어야 한다.
- 즉, 하위 객체에 접근할 때 그 상위 객체의 인터페이스로 접근하더라도 아무런 문제가 없이 일관성 있는 행동을 해야 한다.
- 메소드의 사전 조건은 축소되지 않아야 하며, 사후 조건은 확대되지 않아야 한다.
- 리스코프 치환 원칙을 통해 **다형성**과 **확장성**을 극대화 가능
- 객체 간 is-a 관계일 때만 상속 관계로 모델링 한다.
- 하위 클래스의 공통된 연산을 인터페이스로 제공하고, 구분할 수 있는 멤버를 둔다.
- 하위 클래스는 확장만 수행해야 하며, 상위 클래스의 책임을 무시할 수 없다.
- 하위 클래스가 상속받은 기능 외 필요한게 있다면 구체화(implements) 이용
```
void f(){
  LinkedList list = new LinkedList();
  //...
  modify(list);
}
void modify(LinkedList list){
  list.add(...);
  doMethod(list);
}
```
-> LinkedList의 속도개선을 위해 HashSet을 사용한다면? 
-> LinkedList와 HashSet 모두 Collection Interface를 상속
```
void f(){
  Collection collection = new HashSet();
  //...
  modify(list);
}
void mofidy(Collection collection){
  collection.add(..);
  doMethod(collection);
}
```
-> 이렇게 Collection 생성 부분을 바꿔주면 어떤 컬렉션 클래스든 사용할 수 있다.

## 인터페이스 분리 원칙
- **필요하지 않는 요소를 구현하도록 강요하거나 사용하지 않는 요소에 의존하도록 만들면 안된다.**
- 어떤 클래스가 다른 클래스에 종속될 때에는 가능한 최소한의 인터페이스만 사용
- 인터페이스의 크기를 최소화
- 한 덩어리의 복잡한 인터페이스를 목적에 따라 구분하여 나눈다 ( 상속 , 위임을 통해)
- 기존
```
phone{
  call()
  sms()
  alarm()
}
```
- 변경
```
Call{
  call()
}
Sms{
  sms()
}
Alarm{
  alarm()
}
```

## 의존성 역전 원칙
- 상위 모듈이 하위 모듈에 종속성을 가져서는 안되며, 양쪽 모두 추상화에 의존해야 한다.
- 즉, 하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 구조적 문제에서 발생하는 위계르 끊는 것
- 실제 사용 관계는 바뀌지 않으며, 추상을 매개로 메시지를 주고 받음으로써 관계를 최대한 느슨하게 만든다
- 구성에 대한 설정이 편리해지고 모듈을 테스트하기 쉽다.
- 적용을 위해 추상적인 계층을 만든다.
- ![image](https://user-images.githubusercontent.com/81352078/116171768-5b852800-a744-11eb-9a0a-b81863650d11.png)
