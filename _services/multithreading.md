---
title: "Multithreading"
date: 2018-11-18T12:33:46+10:00
weight: 1
---

# Real-Life Example

**Restaurant Kitchen Scenario:** Imagine a busy restaurant kitchen. The head chef is like the main thread, overseeing everything and ensuring that dishes are prepared correctly. But to keep the kitchen running smoothly and handle many orders efficiently, the chef needs a team of specialized cooks.

## Threads in the Kitchen:

- **Prep Cook (Thread 1):** This cook handles chopping vegetables and preparing ingredients. This task can be done independently of the actual cooking.

- G**rill Chef (Thread 2):** This cook is focused on grilling steaks and burgers. They don’t need to worry about the salads or soups being prepared elsewhere.

- S**auce Maker (Thread 3):** This cook is responsible for making sauces and dressings. Their task is separate from grilling and prepping but essential for completing the dishes.

- **Pastry Chef (Thread 4):** This chef is in charge of preparing desserts. They work independently from the main cooking processes but contribute to the overall meal experience.

In this kitchen, multiple tasks are being handled at the same time by different workers. This speeds up the process and ensures that orders are completed more quickly.

## Multithreading in Computing:

- **Main Thread (Head Chef):** Manages the overall execution and coordination of the program.
- **Worker Threads (Kitchen Staff):** Perform specific tasks (like handling different requests or performing different operations) simultaneously, improving efficiency and performance.

Multithreading is a programming concept where multiple threads are executed concurrently. Threads are the smallest unit of execution within a process. Multithreading allows a program to perform multiple operations simultaneously, making better use of system resources and potentially improving performance.

![Multithreading](/images/multithreading/multithreading.jpeg)

# When to Use Multithreading

- Independent Jobs: If you have two or more jobs that are independent of each other (i.e., their execution doesn't affect one another), you can use multithreading to execute them concurrently. This can lead to better utilization of CPU resources and faster execution.

- Order Not Preserved: If the order of execution of these jobs is not important or can be handled independently, multithreading is appropriate.

# Creating Threads in Java

In Java, you can create a thread by **extending the Thread class** or **implementing the Runnable interface**.

## Using Thread Class

**1. Extend Thread Class:** You create a new class that extends Thread and override the run method.

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        // Code to execute in the new thread
        System.out.println("Thread is running.");
    }
}
```

**2. Start the Thread:** In your main method or another thread, you create an instance of your thread class and call start() to begin execution.

```java
public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // This will invoke the run method in a new thread
    }
}
```

## Using Runnable Interface

**1. Implement Runnable Interface:** You create a class that implements Runnable and define the run method.

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        // Code to execute in the new thread
        System.out.println("Runnable thread is running.");
    }
}
```

 **2. Create and Start Thread:** You create a Thread object, passing an instance of your Runnable implementation, and then start the thread.

```java
public class Main {
    public static void main(String[] args) {
        Runnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);
        thread.start(); // This will invoke the run method in a new thread
    }
}
```

# Key Points

- **run() Method:** This method contains the code that will be executed in the new thread.
- **start() Method:** This method initiates the execution of the thread by invoking the run() method in a new thread of execution.
- **Main Thread:** By default, when you start a new thread, the main thread continues to run concurrently with the new thread.

# Thread Scheduler

The thread scheduler is a component of the Java Virtual Machine (JVM) that manages the execution of threads. Its primary job is to decide the order and timing of thread execution when multiple threads are competing for CPU time.

## Key Points:

- **Scheduling Responsibility:** The thread scheduler decides which thread gets to run and for how long. It handles the switching of threads in and out of the CPU to ensure that all threads get a fair chance to execute.

- **Scheduling Algorithms:** The exact algorithm used by the thread scheduler can vary between different JVM implementations and operating systems. Common algorithms include:

_First-Come, First-Served (FCFS)_,

_Round-Robin Scheduling_,

_Priority-Based Scheduling_.

**Unpredictability:** Because the scheduling algorithm can vary and because thread scheduling can be influenced by factors such as thread priority, system load, and other environmental conditions, the exact order in which threads execute is not guaranteed. This means that multithreaded programs might produce different results each time they run, depending on how threads are scheduled.

**No Guarantees:** You cannot rely on a specific thread execution order. Instead, you should design your multithreaded programs to handle potential variations in execution order. This often involves:

**Synchronization:** Ensuring that shared resources are accessed in a thread-safe manner.
**Concurrency Control:** Using mechanisms like locks, semaphores, or concurrent data structures to manage access to shared resources.

## Example

Consider a scenario where you have two threads, ThreadA and ThreadB. Both threads are designed to print messages to the console. Since the thread scheduler controls their execution, the output might appear in different orders each time you run the program.

```java
public class ThreadExample {
    public static void main(String[] args) {
        Thread threadA = new Thread(() -> System.out.println("Thread A"));
        Thread threadB = new Thread(() -> System.out.println("Thread B"));
        
        threadA.start();
        threadB.start();
    }
}
```

_In the example above, the output could be:_

>Thread A
>
>Thread B

**or**

>Thread B
>
>Thread A

# Objectives

Financial accounting and financial reporting are often used as synonyms.

1. According to International Financial Reporting Standards: the objective of financial reporting is:
2. To provide financial information that is useful to existing and potential investors, lenders and other creditors in making decisions about providing resources to the reporting entity.
3. According to the European Accounting Association:

## Relevance

Relevance is the capacity of the financial information to influence the decision of its users. The ingredients of relevance are the predictive value and confirmatory value. Materiality is a sub-quality of relevance.

> The ingredients of relevance are the predictive value and confirmatory value.

Information is considered material if its omission or misstatement could influence the economic decisions of users taken on the basis of the financial statements.

## Faithful Representation

Faithful representation means that the actual effects of the transactions shall be properly accounted for and reported in the financial statements. The words and numbers must match what really happened in the transaction. The ingredients of faithful representation are completeness, neutrality and free from error.

## Enhancing Qualitative Characteristics

### Verifiability

Verifiability implies consensus between the different knowledgeable and independent users of financial information. Such information must be supported by sufficient evidence to follow the principle of objectivity.

### Comparability

Comparability is the uniform application of accounting methods across entities in the same industry. The principle of consistency is under comparability. Consistency is the uniform application of accounting across points in time within an entity.

### Understandability

Understandability means that accounting reports should be expressed as clearly as possible and should be understood by those to whom the information is relevant.
Timeliness: Timeliness implies that financial information must be presented to the users before a decision is to be made.

---

## Statement of cash flows

The statement of cash flows considers the inputs and outputs in concrete cash within a stated period. The general template of a cash flow statement is as follows: Cash Inflow - Cash Outflow + Opening Balance = Closing Balance

| Cash Inflow | Outflow   | Opening Balance |
| ----------- | --------- | --------------- |
| _Monday_    | `Tuesday` | **Wednesday**   |
| 1           | 2         | 3               |

**Example 1:** in the beginning of September, Ellen started out with $5 in her bank account. During that same month, Ellen borrowed $20 from Tom. At the end of the month, Ellen bought a pair of shoes for $7. Ellen's cash flow statement for the month of September looks like this:

- Cash inflow: $20
- Cash outflow:$7
- Opening balance: $5
- Closing balance: $20 – $7 + $5 = $18

**Example 2:** in the beginning of June, WikiTables, a company that buys and resells tables, sold 2 tables. They'd originally bought the tables for $25 each, and sold them at a price of $50 per table. The first table was paid out in cash however the second one was bought in credit terms. WikiTables' cash flow statement for the month of June looks like this:

> **Important:** the cash flow statement only considers the exchange of actual cash, and ignores what the person in question owes or is owed.

## Statement of financial position (balance sheet)

The balance sheet is the financial statement showing a firm's assets, liabilities and equity (capital) at a set point in time, usually the end of the fiscal year reported on the accompanying income statement.

- **fixed assets**
  - property
  - building
  - equipment (such as factory machinery)
- **intangible assets**
  - copyrights
  - trademarks
  - patents
    - pending
    - international
- goodwill

Owner's equity, sometimes referred to as net assets, is represented differently depending on the type of business ownership. Business ownership can be in the form of a sole proprietorship, partnership, or a corporation. For a corporation, the owner's equity portion usually shows common stock, and retained earnings (earnings kept in the company). Retained earnings come from the retained earnings statement, prepared prior to the balance sheet.
