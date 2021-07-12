## Question Link:
https://leetcode.com/problems/print-in-order/

## Question type: 
Concurrency/ Multithreading

## Question:
Suppose we have a class:
```java
public class Foo {
  public void first() { print("first"); }
  public void second() { print("second"); }
  public void third() { print("third"); }
}
```
The same instance of `Foo` will be passed to three different threads. Thread A will call `first()`, thread B will call `second()`, and thread C will call `third()`. 
Design a mechanism and modify the program to ensure that `second()` is executed after `first()`, and `third()` is executed after `second()`.

## Solution
```java
class Foo {
    private boolean first;
    private boolean second;
    
    public Foo() {
        first=false;
        second=false;        
    }

    public synchronized void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        first=true;
        notifyAll();
    }

    public synchronized void second(Runnable printSecond) throws InterruptedException {
        
        while(!first){ wait();}
        
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        second=true;
        notifyAll();
    }

    public synchronized void third(Runnable printThird) throws InterruptedException {
        while(!second){ wait();}
        
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
}
```
