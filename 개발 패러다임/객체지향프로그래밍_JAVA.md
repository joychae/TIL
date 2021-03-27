
### **01\. Java 문법을 활용해 정의하는 객체 지향 프로그래밍**

Procedure Programming(절차 지향 프로그래밍)은 메소드를 이용해 작은 부품을 만들고, 이를 결합해 더 큰 프로그램을 만들어가는 것이다.

> 몇몇 컴퓨터 엔지니어들은 method만으로 프로그램을 만들어 나가는 것에 부족함을 느꼈습니다.

그래서 프로그래머들은 서로 연관된 변수들과 메소드들을 모아서 그룹핑하고 거기에 이름을 붙여 정리 정돈을 하고 싶어졌다. 그래서 만든 수납상자가 Class이다. Class를 중심으로 프로그램의 구조를 만들어 가는 컴퓨터 프로그래밍 방법론을 Orbject Oreiented Programming(객체지향 프로그래밍)이라 한다.

### **02\. 남의 프로젝트와 남의 인스턴스**

```
import java.io.FileWriter;
import java.io.IOException;
 
public class OthersOOP {
 
    public static void main(String[] args) throws IOException {
        // class : System, Math, FileWriter
        // instance : f1, f2
         
        System.out.println(Math.PI);
        System.out.println(Math.floor(1.8));
        System.out.println(Math.ceil(1.8));
         
        FileWriter f1 = new FileWriter("data.txt");
        f1.write("Hello");
        f1.write(" Java");
         
         
        FileWriter f2 = new FileWriter("data2.txt");
        f2.write("Hello");
        f2.write(" Java2");
        f2.close();
         
        f1.write("!!!");
        f1.close();
    }

}
```

남의 Class인 Math Class를 가져와서 floor, ceil등의 method를 바로바로 사용할 수 있다.

남의 Class인 FileWiter Class를 가져와서 f1, f2등의 복제본을 생성할 수 있다. 이 복제본을 "인스턴스"라 부른다. 긴 맥락에서 작업할 경우 클래스를 직접 생성하지 않고, 복제본을 만들어서 이를 제어하는 방식으로 사용한다.

### **03\. 변수와 메소드, 그리고 클래스**

클래스는 객체 지향의 중심에 있다.

> 우리는 왜 클래스를 사용하는가?

A: 코드들을 기능별로 정리해 깔끔하게 만들고, 재사용성을 높이기 위해서.

```
class Print{
    public static String delimiter = "";
    public static void A() {
        System.out.println(delimiter);
        System.out.println("A");
        System.out.println("A");
    }
    public static void B() {
        System.out.println(delimiter);
        System.out.println("B");
        System.out.println("B");
    }
}

public class MyOOP {
    public static void main(String[] args) {
        Print.delimiter = "----";
        Print.A();
        Print.A();
        Print.B();
        Print.B();
         
        Print.delimiter = "****";
        Print.A();
        Print.A();
        Print.B();
        Print.B();
    }
}
```

예제 코드에서 delimiter라는 매개변수는 printA와 printB에 사용되는데, 매개변수를 메소드 안에 정의하면 번거롭고 유지보수가 힘들다. 따라서 Print라는 클래스를 생성하여 Print클래스 소속 변수인 delimiter를 String 타입으로 선언하고 A와 B로 나누어 클래스 안에 메소드를 형성하였다. 그리고 메인메소드 안에서는 Print소속 변수와 메소드를 이용하여 코드를 깔끔하게 만들었다.

위와 같은 형태로 메인 메소드 안에 모든걸 다 구현하려 하기보다는, class를 만들어서 변수와 메소드를 그 안에 만든다. 이후 메인에서 그 메소드를 호출하는 형태로 짜는게 더 정리정돈된 코드다.

### **04\. 인스턴스**

[##_Image|kage@xx47b/btq0SlpKA3d/Rgt4nta0bvJMdVr1Amtmh1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]

앞에서 배운 클래스는 메소드와 변수들의 모음이다. 다만, 이를 재활용하려 하면 parameter에 값을 넣어주는 것부터 시작하여 일일히 다시 수정해야 하는 복잡다단한 과정을 거져야 한다.

인스턴스는 이러한 클래스의 단점을 보완하기 위하여 등장했다. 클래스를 복제하여 클래스의 성질은 그대로 이용하되, 세부적인 내부 데이터만 바꾸어서 유지시키는 것이다. 이 과정에서 중복이 한번 더 제거되고 코드를 훨씬 더 깔끔하게 작성할 수 있다. 따라서 클래스의 복제본인 인스턴스는 원형인 클래스와 다른 상태를 가지지만, 동일한 기능을 수행한다.

인스턴스가 클래스의 변수나 메소드를 이용하기 위해서는 클래스에서 static으로 선언된 부분의 static을 삭제해주어야 한다. static은 복제를 못하게 막아놓은 특허권과 같다. "원형의 클래스에만 적용된다"라는 의미로 변수와 메소드 선언할 때 함께 붙여 사용할 수 있다.

```
public class MyOOP {
    public static void main(String[] args) {
        Print p1 = new Print();
        p1.delimiter = "----"; // 사용자가 이 과정을 까먹지 않게 하기 위해 나중가면 Print에 기본 생성자를 넣어준다
        p1.A();
        p1.A();
        p1.B();
        p1.B();
 
        Print p2 = new Print();
        p2.delimiter = "****";
        p2.A();
        p2.A();
        p2.B();
        p2.B();
         
         
        p1.A();
        p2.A();
        p1.A();
        p2.A();
    }
```

**인스턴스 관련 이모저모 (생활코딩 싱와님 댓글 출처)**

클래스가 무엇이었나. 번잡한 변수들과 메소드들을 모아서 잘 정리한 서랍 아니었나. 그런데 집 서랍을 잘 보아라, 다양한 서랍이 있다.

이 서랍의 손잡이는 분홍색으로, 저 서랍의 손잡이는 녹색으로 바꾸고 싶은데, "서랍"이라는것은 전세계의 서랍이 될수도있고, 내방 전체의 서랍이 될 수도 있고, 그냥 "서랍"이지 어떤 특정한 서랍은 아니다.

그러다 보니 서랍의 손잡이 색깔을 하나 바꾸려다가 전세계의 서랍의 손잡이 색깔이 죄다 분홍색이 되버릴수도, 녹색이 되버릴수도 있다. 우리집 수납의 손잡이가 죄다 분홍색이라니.. 생각만해도 끔찍해진다.

그래서 인스턴스 개념이 등장했다. 강의에서는 복제품 냉장고에 대한 이야기를 했다. 이를 좀 더 풀어나가서 방금 이야기했던 서랍 이야기로 돌아가보자. 서랍의 손잡이 색깔을 하나 바꾸려고 하니까, 아까는 "서랍"이 전체를 지칭하는(클래스) 범위였기 때문에 모든 손잡이 색깔이 바뀌는 불상사가 일어났었다.

그러나, 이제는 딱 하나의 서랍을 지정하는거다. 그리고 걔 이름을 붙여준다. p1, p2 와 같이.. 그래서 이제는 손잡이를 바꾸는 업자에게 확실하게 이야기할 수 있는 당당함이 생긴다.

"p1이라는 별명을 가진 서랍의 손잡이를 분홍색으로 바꾸어 주세요.." 라고.. p1이라는 별명을 가졌지만 얘도 서랍은 서랍이다. 이제 분홍색 손잡이 서랍이 필요할때마다 전세계의 서랍의 손잡이 색깔을 변경할 필요 없다.

sonjabiColor p1 = new sonjabiColor();

이렇게 하면 정확하게 우리는 어떤 손잡이의 컬러를 바꿀지 업자에게 지칭해주는 것이다. 그러면 기존 서랍의 성질도 모두 가지고 있으면서도, 손잡이의 컬러만 바꿀 수 있는 엄청난 혁명을 겪는것이다!

### **05\. static**

static이 있는 것은 클래스 소속, 없는 것은 인스턴스 소속이다.

데이터 값을 인스턴스에 저장해 계속 변경할 것은 인스턴스 변수, 메소드로 관리하는게 좋다.

반면, 하나의 값이 전체 클래스 모두에게 공통적으로 부여되고, 변함이 없다면 클래스 변수, 메소드로 관리하는 게 좋다.

[##_Image|kage@cjAJiU/btq0Okd6Xot/V7iKjFJgH1DeMfJVnyVqEK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]

### **06\. 생성자와 this**

어떤 객체를 만들때, 그 객체를 생성하기 위해 반드시 해야 할 작업이 있을 것이다. 반드시 해야 할 과정들을 별도의 메소드(=생성자)로 만들어서 객체를 사용하는 사용자가 절차를 생략해도 반드시 해야 할 일들을 놓치지 않게 함으로서 오류를 줄이고 편의성을 증대시킨다.

this.title은 클래스의 title변수를 의미한다.

\[이 글은 생활코딩 자바객체지향프로그래밍 강의를 기반으로 쓰여진 글입니다.\]