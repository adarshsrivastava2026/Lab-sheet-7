# Lab-sheet-7
code
# FOUNDATION OF JAVA LAB SHEET – 7
## Topic: Multithreading

### Q1. Creating Thread by Extending Thread Class

```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Adarsh");
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

**Output:**
```text
Adarsh
Adarsh
Adarsh
Adarsh
Adarsh
```

### Q2. Creating Thread Using Runnable Interface

```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Adarsh");
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

**Output:**
```text
Adarsh
Adarsh
Adarsh
Adarsh
Adarsh
```

### Q3. Thread Name and Priority

```java
public class Main {
    public static void main(String[] args) {
        Thread t = Thread.currentThread();

        System.out.println("Thread Name: " + t.getName());
        System.out.println("Thread Priority: " + t.getPriority());

        t.setName("MyMainThread");

        System.out.println("New Thread Name: " + t.getName());
    }
}
```

**Output:**
```text
Thread Name: main
Thread Priority: 5
New Thread Name: MyMainThread
```

### Q4. Creating Two Threads with Count

```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(getName() + " : " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setName("Thread 1");
        t2.setName("Thread 2");

        t1.start();
        t2.start();
    }
}
```

**Output (Sample):**
```text
Thread 1 : 1
Thread 2 : 1
Thread 1 : 2
Thread 2 : 2
Thread 1 : 3
Thread 2 : 3
Thread 1 : 4
Thread 2 : 4
Thread 1 : 5
Thread 2 : 5
```

### Q5. Three Threads with Random Sleep

```java
import java.util.Random;

class MyThread extends Thread {
    MyThread(String name) {
        super(name);
    }

    public void run() {
        Random r = new Random();
        int time = r.nextInt(501);

        try {
            Thread.sleep(time);
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println(getName() + " is executing.");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread("Reader");
        MyThread t2 = new MyThread("Writer");
        MyThread t3 = new MyThread("Logger");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

**Output (Sample):**
```text
Writer is executing.
Logger is executing.
Reader is executing.
```

### Q6. Demonstrating isAlive()

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running.");

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("Thread completed.");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();

        System.out.println("Before start: " + t.isAlive());

        t.start();

        System.out.println("While running: " + t.isAlive());

        try {
            t.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("After finish: " + t.isAlive());
    }
}
```

**Output (Typical):**
```text
Before start: false
Thread is running.
While running: true
Thread completed.
After finish: false
```

### Q7. Demonstrating join()

```java
class MyThread extends Thread {
    public void run() {
        long sum = 0;

        for (int i = 1; i <= 10000; i++) {
            sum = sum + i;
        }

        System.out.println("Sum = " + sum);
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();

        try {
            t.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("Task finished");
    }
}
```

**Output:**
```text
Sum = 50005000
Task finished
```

### Q8. Thread Priority

```java
class MyThread extends Thread {
    public void run() {
        System.out.println(getName() + " is running.");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setName("High Priority Thread");
        t2.setName("Low Priority Thread");

        t1.setPriority(Thread.MAX_PRIORITY);
        t2.setPriority(Thread.MIN_PRIORITY);

        System.out.println(t1.getName() + " Priority: " + t1.getPriority());
        System.out.println(t2.getName() + " Priority: " + t2.getPriority());

        t1.start();
        t2.start();
    }
}
```

**Output (Sample):**
```text
High Priority Thread Priority: 10
Low Priority Thread Priority: 1
High Priority Thread is running.
Low Priority Thread is running.
```

### Q9. Five Threads with Different Priorities

```java
class MyThread extends Thread {
    public void run() {
        System.out.println(getName() + " Priority: " + getPriority());

        for (int i = 1; i <= 3; i++) {
            System.out.println(getName() + " Count: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();
        MyThread t4 = new MyThread();
        MyThread t5 = new MyThread();

        t1.setName("Thread 1");
        t2.setName("Thread 2");
        t3.setName("Thread 3");
        t4.setName("Thread 4");
        t5.setName("Thread 5");

        t1.setPriority(1);
        t2.setPriority(3);
        t3.setPriority(5);
        t4.setPriority(7);
        t5.setPriority(10);

        t1.start();
        t2.start();
        t3.start();
        t4.start();
        t5.start();
    }
}
```

**Output (Sample):**
```text
Thread 5 Priority: 10
Thread 3 Priority: 5
Thread 1 Priority: 1
Thread 4 Priority: 7
Thread 2 Priority: 3
```

### Q10. Race Condition in BankAccount (Without synchronized)

```java
class BankAccount {
    int balance = 10000;

    void withdraw(int amount) {
        for (int i = 1; i <= 1000; i++) {
            int temp = balance;
            Thread.yield();
            balance = temp - amount;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Thread t1 = new Thread(() -> account.withdraw(1));
        Thread t2 = new Thread(() -> account.withdraw(1));

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("Final Balance: " + account.balance);
        System.out.println("Expected Balance: 8000");
    }
}
```

**Output (Sample):**
```text
Final Balance: 9125
Expected Balance: 8000
```

### Q11. Fixing Race Condition Using synchronized Method

```java
class BankAccount {
    int balance = 10000;

    synchronized void withdraw(int amount) {
        for (int i = 1; i <= 1000; i++) {
            balance = balance - amount;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Thread t1 = new Thread(() -> account.withdraw(1));
        Thread t2 = new Thread(() -> account.withdraw(1));

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("Final Balance: " + account.balance);
    }
}
```

**Output:**
```text
Final Balance: 8000
```

### Q12. Using synchronized Block

```java
class BankAccount {
    int balance = 10000;
    Object lock = new Object();

    void withdraw(int amount) {
        for (int i = 1; i <= 1000; i++) {
            synchronized (lock) {
                balance = balance - amount;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Thread t1 = new Thread(() -> account.withdraw(1));
        Thread t2 = new Thread(() -> account.withdraw(1));

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("Final Balance: " + account.balance);
    }
}
```

**Output:**
```text
Final Balance: 8000
```

### Q13. Producer-Consumer Using wait() and notify()

```java
class Buffer {
    int data;
    boolean available = false;

    synchronized void produce(int value) {
        try {
            while (available) {
                wait();
            }

            data = value;
            System.out.println("Produced: " + data);

            available = true;
            notify();

        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    synchronized void consume() {
        try {
            while (!available) {
                wait();
            }

            System.out.println("Consumed: " + data);

            available = false;
            notify();

        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}

class Producer extends Thread {
    Buffer buffer;

    Producer(Buffer buffer) {
        this.buffer = buffer;
    }

    public void run() {
        for (int i = 1; i <= 10; i++) {
            buffer.produce(i);
        }
    }
}

class Consumer extends Thread {
    Buffer buffer;

    Consumer(Buffer buffer) {
        this.buffer = buffer;
    }

    public void run() {
        for (int i = 1; i <= 10; i++) {
            buffer.consume();
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Buffer buffer = new Buffer();

        Producer p = new Producer(buffer);
        Consumer c = new Consumer(buffer);

        p.start();
        c.start();
    }
}
```

**Output:**
```text
Produced: 1
Consumed: 1
Produced: 2
Consumed: 2
Produced: 3
Consumed: 3
Produced: 4
Consumed: 4
Produced: 5
Consumed: 5
Produced: 6
Consumed: 6
Produced: 7
Consumed: 7
Produced: 8
Consumed: 8
Produced: 9
Consumed: 9
Produced: 10
Consumed: 10
```

### Q14. Creating Deadlock Using Two Shared Objects

```java
import java.util.concurrent.CyclicBarrier;

public class Main {
    static final Object Lock1 = new Object();
    static final Object Lock2 = new Object();

    static CyclicBarrier barrier = new CyclicBarrier(2);

    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (Lock1) {
                System.out.println("Thread 1 acquired Lock1");

                try {
                    barrier.await();
                } catch (Exception e) {
                    return;
                }

                synchronized (Lock2) {
                    System.out.println("Thread 1 acquired Lock2");
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized (Lock2) {
                System.out.println("Thread 2 acquired Lock2");

                try {
                    barrier.await();
                } catch (Exception e) {
                    return;
                }

                synchronized (Lock1) {
                    System.out.println("Thread 2 acquired Lock1");
                }
            }
        });

        t1.start();
        t2.start();
    }
}
```

**Output:**
```text
Thread 1 acquired Lock1
Thread 2 acquired Lock2
```

### Q15. Fixing Deadlock by Acquiring Locks in Same Order

```java
public class Main {
    static final Object Lock1 = new Object();
    static final Object Lock2 = new Object();

    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (Lock1) {
                System.out.println("Thread 1 acquired Lock1");

                synchronized (Lock2) {
                    System.out.println("Thread 1 acquired Lock2");
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized (Lock1) {
                System.out.println("Thread 2 acquired Lock1");

                synchronized (Lock2) {
                    System.out.println("Thread 2 acquired Lock2");
                }
            }
        });

        t1.start();
        t2.start();
    }
}
```

**Output (Sample):**
```text
Thread 1 acquired Lock1
Thread 1 acquired Lock2
Thread 2 acquired Lock1
Thread 2 acquired Lock2
```

---

