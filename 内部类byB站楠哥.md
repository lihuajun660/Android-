1 内部类
====================
一般情况下，类和类之间是相互独立的，

1、非静态内部类
```java
public class OuterClass {
    //成员变量
    private String outerName;
    //成员方法
    public void display(){
        System.out.println("OuterClass display");
        System.out.println(outerName);
    }
    //内部类
    public class InnerClass{
        //成员变量
        private String InnerName;
        //成员方法
        public void display(){
            System.out.println("InnerClass display");
            System.out.println(InnerName);
        }
        public InnerClass(){
            InnerName = "inner Class";
        }

    }

    public static void main(String[] args) {
        OuterClass outerClass = new OuterClass();
        outerClass.display();
        OuterClass.InnerClass innerClass = outerClass.new InnerClass();
        innerClass.display();
    }
}
```

将内部类当做外部类的一个成员变量/成员方法来使用，所以必须依赖于外部类的对象才能调用，用法和成员变量是一致的。

1.1 为什么要使用内部类？
===============
采用内部类这种技术，可以隐藏细节和内部结构，封装性更好，让程序的结构更加合理。

基本的内部类还能在一个方法体中



2、 静态内部类
===================
静态内部类的构造不需要依赖于外部类的对象，类中的所有静态组建都不需要依赖于任何对象，可以直接通过类本身进行构造。

```java
public class OuterClass {
    //成员变量
    private String outerName;
    //成员方法
    public void display(){
        System.out.println("OuterClass display");
        System.out.println(outerName);
    }

    public static class InnerClass{
        private String innerName;
        public InnerClass(){
            innerName = "inner class";
        }
        public void display(){
            System.out.println("InnerClass display");
            System.out.println(innerName);
        }
    }


    public static void main(String[] args) {
        OuterClass outerClass = new OuterClass();
        outerClass.display();
        OuterClass.InnerClass innerClass = new InnerClass();
        innerClass.display();
    }
}
```


3、匿名内部类
===================
```java
        MyInterface myInterface1 = new MyInterface() {
            @Override
            public void test() {
                System.out.println("test2");
            }
        };

```
