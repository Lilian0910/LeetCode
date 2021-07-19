## Question Link:
https://leetcode.com/problems/fizz-buzz-multithreaded/

## Question type: 
Concurrency/ Multithreading

## Question:
You have the four functions:

* `printFizz` that prints the word "Fizz" to the console,
* `printBuzz` that prints the word "Buzz" to the console,
* `printFizzBuzz` that prints the word "FizzBuzz" to the console, and
* `printNumber` that prints a given integer to the console.    

You are given an instance of the class `FizzBuzz` that has four functions: `fizz`, `buzz`, `fizzbuzz` and `numbe`r. The same instance of `FizzBuzz` will be passed to four different threads:

* **Thread A:** calls `fizz()` that should output the word "Fizz".
* **Thread B:** calls `buzz()` that should output the word "Buzz".
* **Thread C:** calls `fizzbuzz()` that should output the word "FizzBuzz".
* **Thread D:** calls `number()` that should only output the integers.    

Modify the given class to output the series `[1, 2, "Fizz", 4, "Buzz", ...]` where the `ith` token (1-indexed) of the series is:

* "FizzBuzz" if i is divisible by 3 and 5,
* "Fizz" if i is divisible by 3 and not 5,
* "Buzz" if i is divisible by 5 and not 3, or
* i if i is not divisible by 3 or 5.

Implement the `FizzBuzz` class:

* `FizzBuzz(int n)` Initializes the object with the number n that represents the length of the sequence that should be printed.
* `void fizz(printFizz)` Calls `printFizz` to output "Fizz".
* `void buzz(printBuzz)` Calls `printBuzz` to output "Buzz".
* `void fizzbuzz(printFizzBuzz)` Calls `printFizzBuzz` to output "FizzBuzz".
* `void number(printNumber)` Calls `printnumber` to output the numbers.

## Solution  
### 1. use synchronized lock
```java
class FizzBuzz {
    
    private int n;
    private int num = 1;
    
    public FizzBuzz(int n) {
        this.n = n;
    }

    // printFizz.run() outputs "fizz".
    public synchronized void fizz(Runnable printFizz) throws InterruptedException {
        while (num <= n) {
            if (num % 3 != 0 || num % 5 == 0) {
                wait();
                continue;
            }
            printFizz.run();
            num += 1;
            notifyAll();
        }
    }

    // printBuzz.run() outputs "buzz".
    public synchronized void buzz(Runnable printBuzz) throws InterruptedException {
        while (num <= n) {
            if (num % 5 != 0 || num % 3 == 0) {
                wait();
                continue;
            }
            printBuzz.run();
            num += 1;
            notifyAll();
        }
    }

    // printFizzBuzz.run() outputs "fizzbuzz".
    public synchronized void fizzbuzz(Runnable printFizzBuzz) throws InterruptedException {
        while (num <= n) {
            if (num % 15 != 0) {
                wait();
                continue;
            }
            printFizzBuzz.run();
            num += 1;
            notifyAll();
        }
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public synchronized void number(IntConsumer printNumber) throws InterruptedException {
        while (num <= n) {
            if (num % 3 == 0 || num % 5 == 0) {
                wait();
                continue;
            }
            printNumber.accept(num);
            num += 1;
            notifyAll();
        }
    }
}
```
### 2. use semaphore
```java
class FizzBuzz {
    private int n;
	private Semaphore fizz = new Semaphore(0);
	private Semaphore buzz = new Semaphore(0);
	private Semaphore fizzbuzz = new Semaphore(0);
	private Semaphore num = new Semaphore(1);

	public FizzBuzz(int n) {
        this.n = n;
    }

	// printFizz.run() outputs "fizz".
	public void fizz(Runnable printFizz) throws InterruptedException {
		for (int k = 1; k <= n; k++) {
			if (k % 3 == 0 && k % 5 != 0) {
				fizz.acquire();
				printFizz.run();
				releaseLock(k + 1);
			}
		}
	}

	// printBuzz.run() outputs "buzz".
	public void buzz(Runnable printBuzz) throws InterruptedException {
		for (int k = 1; k <= n; k++) {
			if (k % 5 == 0 && k % 3 != 0) {
				buzz.acquire();
				printBuzz.run();
				releaseLock(k + 1);
			}
		}
	}

	// printFizzBuzz.run() outputs "fizzbuzz".
	public void fizzbuzz(Runnable printFizzBuzz) throws InterruptedException {
		for (int k = 1; k <= n; k++) {
			if (k % 15 == 0) {
				fizzbuzz.acquire();
				printFizzBuzz.run();
				releaseLock(k + 1);
			}
		}
	}

	// printNumber.accept(x) outputs "x", where x is an integer.
	public void number(IntConsumer printNumber) throws InterruptedException {
		for (int k = 1; k <= n; k++) {
			if (k % 3 != 0 && k % 5 != 0) {
				num.acquire();
				printNumber.accept(k);
				releaseLock(k + 1);
			}
		}
	}

	public void releaseLock(int n) {
		if (n % 3 == 0 && n % 5 != 0) {
			fizz.release();
		} else if (n % 5 == 0 && n % 3 != 0) {
			buzz.release();
		} else if (n % 15 == 0) {
			fizzbuzz.release();
		} else {
			num.release();
		}
	}
}
```
