## Question Link:
https://leetcode.com/problems/print-foobar-alternately/

## Question type: 
Concurrency/ Multithreading

## Question:
Suppose you are given the following code:
```jiava
class FooBar {
  public void foo() {
    for (int i = 0; i < n; i++) {
      print("foo");
    }
  }

  public void bar() {
    for (int i = 0; i < n; i++) {
      print("bar");
    }
  }
}
```
The same instance of `FooBar` will be passed to two different threads. 
Thread A will call `foo()` while thread B will call `bar()`. Modify the given program to output "foobar" n times.

## Solution  
### 1. use synchronized lock
```java
class FooBar {
    private int n;
    private boolean first;
    
    public FooBar(int n) {
        this.n = n;
        this.first=true;
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        
        for (int i = 0; i < n; i++) {
            synchronized(this){
                while(!this.first){this.wait();}
                // printFoo.run() outputs "foo". Do not change or remove this line.
        	    printFoo.run();
                this.first=false;
                this.notifyAll();
            }
        	
        }
    }

    public void bar(Runnable printBar) throws InterruptedException {
        
        for (int i = 0; i < n; i++) {
            synchronized(this){
                while(this.first){this.wait();}
                // printBar.run() outputs "bar". Do not change or remove this line.
        	    printBar.run();
                this.first=true;
                this.notifyAll();
            }
        }
    }
}
```
### 2. use semaphore
```java
class FooBar {
  private int n;
  private final Semaphore fooSync;
  private final Semaphore barSync;
  
  public FooBar(int n) {
    this.n = n;
    this.fooSync = new Semaphore(1);
    this.barSync = new Semaphore(0);
  }

  public void foo(Runnable printFoo) throws InterruptedException {

    for (int i = 0; i < n; i++) {
      this.fooSync.acquireUninterruptibly();
      // printFoo.run() outputs "foo". Do not change or remove this line.
      printFoo.run();
      this.barSync.release();
    }
  }

  public void bar(Runnable printBar) throws InterruptedException {
    for (int i = 0; i < n; i++) {
      this.barSync.acquireUninterruptibly();
        // printBar.run() outputs "bar". Do not change or remove this line.
      printBar.run();
      this.fooSync.release();
    }
  }
}
```
