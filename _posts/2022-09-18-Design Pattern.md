---
title: 디자인패턴
author: HH KWON
date: 2022-07-29
category: Jekyll
layout: post
---

# Design Pattern

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
    ```
    ```c#
    static void Main(string[] args){
        var objectA = Singleton.Instance();
        var objectB = Singleton.Instance();         // objectA, B 모두 동일한 객체
    }
    ```
<br><br>
2. 팩토리 메서드 패턴
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
{ ... }
}
      
public class Cat : Behave
{
public int Height;
public override void run()
{ ... }
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