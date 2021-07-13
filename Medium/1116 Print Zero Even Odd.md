## Question Link:
https://leetcode.com/problems/print-zero-even-odd/

## Question type: 
Concurrency/ Multithreading

## Question:
You have a function `printNumber` that can be called with an integer parameter and prints it to the console.

For example, calling `printNumber(7)` prints 7 to the console.
You are given an instance of the class `ZeroEvenOd`d that has three functions: `zero`, `even`, and `odd`. The same instance of ZeroEvenOdd will be passed to three different threads:

**Thread A:** calls `zero()` that should only output 0's.   
**Thread B:** calls `even()` that should only output even numbers.    
**Thread C:** calls `odd()` that should only output odd numbers.
Modify the given class to output the series "010203040506..." where the length of the series must be 2n.

Implement the `ZeroEvenOdd` class:

`ZeroEvenOdd(int n)` Initializes the object with the number n that represents the numbers that should be printed.
`void zero(printNumber)` Calls `printNumber` to output one zero.
`void even(printNumber)` Calls `printNumber` to output one even number.
`void odd(printNumber)` Calls `printNumber` to output one odd number.

## Solution  
### 1. use synchronized lock
```java
class ZeroEvenOdd {
    private int n;
    private boolean iszero;
    private enum Type{EVEN, ODD};
    Type nonzero;
    
    public ZeroEvenOdd(int n) {
        this.n = n;
        this.iszero=true;
        this.nonzero=Type.ODD;
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public void zero(IntConsumer printNumber) throws InterruptedException {
        for(int i=0; i<n; i++){
            synchronized(this){
                while(!this.iszero){this.wait();} //while not zero->wait
                printNumber.accept(0); //while zero->print number 0
                this.iszero=false; //after 0, it should be n, so iszero=false
                this.notifyAll();
            }
        }
    }

    public void even(IntConsumer printNumber) throws InterruptedException {
        for(int i=2; i<=n; i+=2){
            synchronized(this){
                while(this.iszero || this.nonzero ==Type.ODD){this.wait();} //while not even-> iszero|| is odd-->wait
                printNumber.accept(i);
                this.iszero=true; //after print i, the next should be zero and next i will be odd
                this.nonzero=Type.ODD;
                this.notifyAll();
            }
        }
    }

    public void odd(IntConsumer printNumber) throws InterruptedException {
        for(int i=1; i<=n; i+=2){
            synchronized(this){
                while(this.iszero || this.nonzero ==Type.EVEN){this.wait();} //while not odd-> iszero|| is even-->wait
                printNumber.accept(i);
                this.iszero=true;
                this.nonzero=Type.EVEN;
                this.notifyAll();
            }
        }
    }
}
```
### 2. use semaphore
```java
class ZeroEvenOdd {
    private int n;
    private Semaphore semZero;
    private Semaphore semOdd;
    private Semaphore semEven;
    
    public ZeroEvenOdd(int n) {
        this.n = n;
        semZero = new Semaphore(1);
        semOdd = new Semaphore(0);
        semEven = new Semaphore(0);
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public void zero(IntConsumer printNumber) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            semZero.acquire();           
            printNumber.accept(0);   
            semOdd.release();
            semEven.release();
        }
    }

    public void even(IntConsumer printNumber) throws InterruptedException {
        for (int i = 1; i <= n; i++) {
            semEven.acquire(); 
            if (i % 2 == 0) {
                printNumber.accept(i);
                semZero.release();
            }
        }
    }

    public void odd(IntConsumer printNumber) throws InterruptedException {
        for (int i = 1; i <= n; i++) {
            semOdd.acquire();            
            if (i % 2 == 1) {
                printNumber.accept(i);
                semZero.release();
            }
        }
    }
}
```
