# Concurrency



# 1.Concurrency: An Overview



## 1.1.Introduction to Concurrency

:pushpin:**What is <u>Concurrency</u>?**

Doing more than one thing at a time.



:pushpin:**Concurrency $\neq$ Multithreading**

Multithreading is one form of concurrency, but certainly <u>**not the only one**</u>.

<img src="img/image-20220105113450589.png" alt="image-20220105113450589" style="zoom: 80%;" />



:pushpin:**What is <u>Multithreading</u>?**

A form of concurrency that uses multiple threads of execution.



:pushpin:**Don't use `Thread()`!!**:warning:

`Thread()` is **<u>outdated</u>**. As soon as you type `new Thread()`, it’s over;:skull: your project already has legacy code.



:pushpin:**What is <u>Parallel processing</u>?**

Doing lots of work by dividing it up among multiple threads that run concurrently.



:pushpin:**Relationship so far**

<img src="img/image-20220105114052995.png" alt="image-20220105114052995" style="zoom:80%;" />



:pushpin:**What is <u>Asynchronous programming</u>?**

A form of concurrency that uses <u>futures</u> or <u>callbacks</u> to **<u>avoid unnecessary threads</u>**.



:pushpin:**What is future?**

A <u>future</u> (or <u>promise</u>) is a type that represents <u>some operation that will complete in the future</u>. Some modern future types in .NET are `Task` and `Task<TResult>`.



:pushpin:**The core of Asynchronous programming**

The core is the idea of an asynchronous operation which is <u>started</u> that will <u>complete some time later</u>.



:pushpin:**What is Reactive Programming?**

A declarative style of programming <u>where the application reacts to events</u>.



:pushpin:**Summary**

![image-20220105134756868](img/image-20220105134756868.png)



:pushpin:**Which technique should we use?**

Generally, most applications use multithreading (via the <u>thread pool</u>) and <u>asynchronous programming</u>.



## 1.2.Introduction to Asynchronous Programming



## 1.3.Introduction to Parallel Programming



## 1.4.Introduction to Reactive Programming (Rx)



## 1.5.Introduction to Dataflows



## 1.6.Introduction to Multithreaded Programming



## 1.7.Modern Design



## 1.8.Summary of Key Technologies



# 2.Async Basics

## 2.1.Pausing for a Period of Time

## 2.2.Returning Completed Tasks

# 3.Asynchronous Streams



# 4.Parallel Basics



# 5.Dataflow Basics



# 6.System.Reactive Basics



# 7.Testing



# 8.Interop



# 9.Collections



# 10.Cancellation



# 11.Functional-Friendly OOP



# 12.Synchronization



# 13.Scheduling



# 14.Scenarios



