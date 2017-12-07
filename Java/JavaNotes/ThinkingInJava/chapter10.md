---
title: 内部类
tags: Java, 内部类
---

# 内部类

可以将一个类的定义放在另一个类的定义内部，这就是内部类。

内部类允许把逻辑相关的类组织在一起，并控制位于内部的类的可视性。

内部类了解外围类（在其中定义该内部类的类），并能与之通信。

## 创建内部类

```java
/**
 * 内部类
 */
//: Parcell.java

 public class Parcell {
     class Contents {
         private int i = 11;
         public int value() { return i; }
     }

     class Destination {
         private String label;
         Destination(String whereTo) {
             label = whereTo;
         }
         String readLine() { return label; }
     }

     public void ship(String dest) {
         Contents c = new Contents();
         Destination d = new Destination(dest);
         System.out.println(d.readLine());
     }

     public static void main(String[] args) {
         Parcell p = new Parcell();
         p.ship("Tasmania");
     }
 } /** Output
Tasmania
*/
```

内部类更典型的用法是，外部类调用一个方法，该方法返回一个指向内部类的引用。

如果想从外部类的非静态方法之外的任意位置创建某个内部类的**对象引用**，那么必须具体指明这个对象的类型，比如：`OuterClassName.InnerClassName`。

## 链接到外部类

当生成一个内部类的对象时，此对象与制造它的外围对象之间就有了一种联系，所以他能访问其外围对象的所有成员，而不需要任何特殊条件。

此外，内部类还拥有其外围类的所有元素的访问权。

```java
//: Sequence.java
interface Selector {
    boolean end();
    Object current();
    void next();
}

public class Sequence {
    private Object[] items;
    private int next = 0;
    public Sequence(int size) {
        items = new Object[size];
    }
    public void add(Object x) {
        if (next < items.length) {
            items[next++] = x;
        }
    }

    private class SequenceSelector implements Selector {
        private int i = 0;
        public boolean end() {
            return i == items.length;
        }

        public Object current() {
            return items[i];
        }

        public void next() {
            if (i < items.length) 
                i++;
        }
    }

    public Selector selector() {
        return new SequenceSelector();
    }

    public static void main(String args[]) {
        Sequence sequence = new Sequence(10);
        for (int i = 0; i < 10; ++i) {
            sequence.add(Integer.toString(i));
        }
        Selector selector = sequence.selector();
        while(!selector.end()) {
            System.out.print(selector.current() + " ");
            selector.next();
        }
    }
} /** Output
0 1 2 3 4 5 6 7 8 9
*/
```

**内部类自动拥有对其外围类所有成员的访问权, 内部类可以访问其外围类的方法和字段, 就像自己拥有它们似的, 这带来了很大的方便.**

当某个外围类的对象创建了一个内部类对象时, 此内部对象必定会秘密地捕获一个指向那个外围类对象的引用. 然后, 在访问此外围类的成员时, 就是用那个引用来选择外围类的成员.

## 使用.this和.new

如果需要生成对外部类对象的引用，可以使用外部类的名字后面紧跟远点和this。这样产生的引用自动地具有正确的类型。

```java
//: DotThis.java
public class DotThis {
    void f() {
        System.out.println("DotThis.f()");
    }
    public class Inner {
        public DotThis outer() {
            return DotThis.this;
            // A plain this would be Inner's this.
        }
    }
    public Inner inner() {
        return new Inner();
    }
    public static void main(String args[]) {
        DotThis dt = new DotThis();
        DotThis.Inner dti = dt.inner();
        dti.outer().f();
    }
} /** Output
DotThis.f()
*/
```

如果要告知其他对象，去创建其某个内部类的对象。要实现此目的，必须在new表达式中提供对其他外部类对象的引用，这时需要使用.new语法。

```java
//: DotNew.java
public class DotNew {
    public class Inner {}
    public static void main(String args[]) {
        DotNew dn = new DotNew();
        DotNew.Inner dni = dn.new Inner();
    }
}
```

创建内部类对象，不是引用外部类的名字（上例中DotNew），而是必须使用外部类的对象来创建该内部类对象。

**在拥有外部类对象之前，是不能创建内部类对象的。因为内部类对象会隐式连接到创建它的外部类对象上。但是如果创建的是嵌套类（静态内部类），那么它就对不需要外部类对象的引用。**

```java
//: DotNew.java
public class DotNew {
    public class Inner {
        public void f() {
            System.out.println("DotNew.Inner.f()");
        }
    }
    public static class StaticInner {
        public void f() {
            System.out.println("DotNew.StaticInner.f()");
        }
    }

    public Inner f() {
        return new Inner();     // 注意这里
    }

    public static void main(String args[]) {
        DotNew dn = new DotNew();
        DotNew.Inner dni = dn.new Inner();
        dni.f();
        //! Inner in = new Inner(); // Error: 无法从静态上下文中引用非静态 变量 this
        //! Inner in = new DotNew.Inner(); // Error: 无法从静态上下文中引用非静态 变量 this
        Inner in = dn.new Inner();
        in.f();

        Inner fin = dn.f();
        fin.f();

        // Inner in2 = new dn.Inner(); // Error: 程序包dn不存在
        StaticInner si = new StaticInner();
        si.f();
    }
} /** Output
DotNew.Inner.f()
DotNew.Inner.f()
DotNew.Inner.f()
DotNew.StaticInner.f()
 */
```

## 内部类和向上转型

如果内部类是某个接口的实现，那么就可以完全不可见，并且不可用。所得到的只是指向基类或接口的引用，所以能够很方便地隐藏实现细节。

```java
//: TestParcel.java

interface Destination {
    String readLabel();     // 接口中所有成员自动设置为public
}

interface Contents {
    int value();
}

class Parcel {
    private class PContents implements Contents {
        private int i = 0;
        public int value() { return i++; }
    }

    protected class PDestination implements Destination {
        private String label;
        private PDestination(String whereTo) {
            label = whereTo;
        }
        public String readLabel() { return label; }
    }

    public Destination destination(String s) {
        return new PDestination(s);
    }

    public Contents contents() {
        return new PContents();
    }
}

public class TestParcel {
    public static void main(String args[]) {
        Parcel p = new Parcel();
        Contents c = p.contents();
        Destination d = p.destination("Beijing");
        System.out.println(c.value());
        System.out.println(d.readLabel());
    }
} /** Output
0
Beijing
*/
```

**private内部类给类设计者提供了一种途径，通过这种方式可以完全阻止任何依赖于类型的编码，并且完全隐藏了实现的细节。**
