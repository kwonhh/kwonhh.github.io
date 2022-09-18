---
title: 디자인패턴
author: HH KWON
date: 2022-07-29
category: Jekyll
layout: post
---

# Design Pattern
1. 분류
- Creational Pattern(생성 패턴)
  - 객체 생성에 관련된 패턴
  - 객체의 생성과 조합을 캡슐화 하여 특정 개체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성 제공
- Structural Pattern(구조 패턴)
  - 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
  - 서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스 제공하거나 객체들을 서로 묶어 새로운 기능 제공
- Behavioral Pattern(행위 패턴)
  - 객체나 클래스 사이의 알고리즘이나 책임 분배에 관련된 패턴
  - 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 그리고 그렇게 하면서도 객체 사이의 결합도를 최소화(느슨한 결합)하는 것에 중점을 둔다<br><br>
  
## Creational Pattern(생성 패턴)
1. Singleton Pattern(싱글턴 패턴)
- 특징
    - 사용하는 객체를 Static으로 선언 -> 해당 객체의 메모리를 정적할당 하면서 하나의 객체에만 접근
    - 다른 곳에서 새롭게 생성자 선언하더라도, 이미 정적 선언된 객체가 반환되므로 중복 선언 방지
- 장점
    - 매우 단순한 구조
    - 모든 데이터에 전역으로 접근 및 관리가 가능
- 단점
    - 정적 메모리에 할당된 객체이므로 해당 객체에 너무 큰 메모리 쌓이게 되면 성능이 저하
    - 따라서 복잡한 프로그램에 이 패턴을 사용하는 경우 효율이 떨어지고<br>서로 다른 데이터를 공유하게 되면 다른 객체들과 결합도가 떨어지게 됨
- 구현

```c#
pravate class Singleton {
    private static Singleton stc_singleton;     // 정적 객체 선언
    public static Singleton Instance() {
        if (stc_singleton == null)
            stc_singleton = new Singleton();    // stc_singleton 객체의 중복선언을 방지
        return stc_singleton;
    }
}

static void Main(string[] args){
    var objectA = Singleton.Instance();
    var objectB = Singleton.Instance();         // objectA, B 모두 동일한 객체
}
```

<br><br>
2. Factory Method Pattern(팩토리 메서드 패턴)
- 특징
    - 해당 클래스를 상속받은 클래스에 객체 생성 방법을 명시. 즉, 생성자를 사용해 객체를 생성하지 않고 그 기능을 파생 클래스에 위임
    - 프로그램의 구조가 잡힌 상태에서 여러사람이 협업하면서 각각의 파생 클래스를 구현하는 것이 가능한 구조
    - 기능의 추가/변경 시 객체 생성코드를 유연하게 변경 가능
- 구현

```c#
// Product 클래스 구현
public abstract class Behave
{
    public abstract void run();
}

// ConcreteProduct 클래스 구현
public class Dog : Behave
{
public int NumOfLeg;
public override void run()
{ System.out.println("Dog is running"); }
}
      
public class Cat : Behave
{
public int Height;
public override void run()
{ System.out.println("Cat is running"); }
} 

// Creator 클래스 구현
public abstract class BehaveCreator
{
    public abstract BehaveCreator();
}

// ConcreteCreator 클래스 구현 : DogCreator
public class DogCreator : BehaveCreator
{
    public override BehaveCreator()
  {
    return new Dog();           // DogCreator의 객체 생성하고, BehaveCreator 실행하면, Dog의 메서드 사용 가능
  }
}
// ConcreteCreator 클래스 구현 : CatCreator
public class CatCreator : BehaveCreator
{
    public override BehaveCreator()
    {
    return new Cat();
    }
}
```

<br><br>
3. Abstract Factory Pattern(추상 팩토리 패턴)
- 특징
  - 구체적인 클래스에 의존하지 않고, 서로 연관되거나 의존적인 객체들의 조합을 만드는 인터페이스
  - 관련성 있는 여러 종류의 객체를 일관된 방식으로 생성하는 경우 유용
- 클래스 다이어크램 UML
  - 출처 : [위키피디아](https://ko.wikipedia.org/wiki/%EC%B6%94%EC%83%81_%ED%8C%A9%ED%86%A0%EB%A6%AC_%ED%8C%A8%ED%84%B4#%ED%81%B4%EB%9E%98%EC%8A%A4_%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8 "위키피디아")<br>
  <img src="../gitbook/images/AbstractFactory_UML.png" width="677" height="448"><br>
  - 추상팩토리 인터페이스에서 CrateProductA, B를 선언하고, 이의 파생클래스 ConcreteFactory1, 2에서는 서로 다른 조건에 따라 생성 함수를 구현할 수 있음
  - 예를 들어 선풍기 부품을 납품한다고 했을 때, 선풍기의 모터, 날개 등의 기능은 동일할 수 있지만, 각각의 규격은 납품하는 회사마다 달라질 수 있다
- 구현 예시

```c#
// 출처 : 위키피디아, https://ko.wikipedia.org/wiki/%EC%B6%94%EC%83%81_%ED%8C%A9%ED%86%A0%EB%A6%AC_%ED%8C%A8%ED%84%B4#%ED%81%B4%EB%9E%98%EC%8A%A4_%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8

interface IButton
{
    void Paint();
}

interface IGUIFactory
{
    IButton CreateButton();
}

class WinFactory : IGUIFactory
{
    public IButton CreateButton()
    {
        return new WinButton();
    }
}

class OSXFactory : IGUIFactory
{
    public IButton CreateButton()
    {
        return new OSXButton();
    }
}

class WinButton : IButton
{
    public void Paint()
    {
        //Render a button in a Windows style
    }
}

class OSXButton : IButton
{
    public void Paint()
    {
        //Render a button in a Mac OS X style
    }
}

class Program
{
    static void Main()
    {
        var appearance = Settings.Appearance;

        IGUIFactory factory;
        switch (appearance)
        {
            case Appearance.Win:
                factory = new WinFactory();
                break;
            case Appearance.OSX:
                factory = new OSXFactory();
                break;
            default:
                throw new System.NotImplementedException();
        }

        var button = factory.CreateButton();
        button.Paint();
    }
}
```

<br><br>
4. Builder Pattern(빌더 패턴)
5. ProtoType(프로토 타입)

<br><br>
## Structural Pattern(구조 패턴)
1. Adapter Pattern(어댑터 패턴)
2. Bridge Pattern(브릿지 패턴)
3. Composite Pattern(컴퍼지트 패턴)
4. Decorator Pattern(데코레이터 패턴)
5. Facade Pattern(퍼사드 패턴)
6. FlyWeight Pattern(플라이웨이트 패턴)
7. Proxy Pattern(프록시 패턴)
