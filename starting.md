### What is this?

discharge: sometimes I'll copy and paste from the references page for the sake of saving time... this is a personal journey...

So,** what is Reactive programming**?

"Reactive programming is programming with asynchronous data streams \(AD$\)."

e.g.: click events are really an asynchronous event stream, on which _you can observe and do some side effects_

You are able to create data streams \(D$\) of anything...

**On top of that, you are given an amazing toolbox of functions to combine, create and filter any of those streams.**

That's where the "functional" magic kicks in. A stream can be used as an input to another one. Even multiple streams can be used as inputs to another stream. You can \_merge \_two streams. You can \_filter \_a stream to get another one that has only those events you are interested in. You can \_map \_data values from one stream to another new one.

A stream is a sequence of **ongoing events ordered in time**. It can emit three different things: a value \(of some type\), an error, or a "completed" signal. Consider that the "completed" takes place, for instance, when the current window or view containing that button is closed.

We capture these emitted events only **asynchronously**, by defining a function that will execute when a value is emitted, another function when an error is emitted, and another function when 'completed' is emitted. Sometimes these last two can be omitted and you can just focus on defining the function for values. The "listening" to the stream is called **subscribing**. The functions we are defining are observers. The stream is the subject \(or "observable"\) being observed. This is precisely the [Observer Design Pattern](https://en.wikipedia.org/wiki/Observer_pattern).

There is different ways to visualize streams...

Marble diagrams...

![](/assets/Screen Shot 2017-07-12 at 12.08.49.png)ASCII...

```
--a---b-c---d---X---|->

a, b, c, d are emitted values
X is an error
| is the 'completed' signal
---> is the timeline
```

Some Terms:

* **Observable: **represents the idea of an invokable collection of future values or events.

  In other words: its a wrapper around some data source \\( **stream** of values , async -usually - or not \)

* **Observer: **is a collection of callbacks that knows how to listen to values delivered by the Observable.

  In other words: we want to **do something whenever a new value occurs**. The observer execute some code whenever we receive a new value, or an error, or if the observable reports that is done.

* **Subscription:** represents the execution of an Observable, is primarily useful for cancelling the execution.

  In other words: the subscription is **the connection** between Observable and Observer

the** next method** will be called by the observable whenever a new value is emitted \(whenever we receive a new value\)

the **error method** will be called whenever the observable throws an error

the **complete method** will be called whenever the observable is done

* **Operators: **are **pure functions** that enable a functional programming style of dealing with collections with operations like `map`, `filter`, `concat`, `flatMap` , etc.

* **Subject: **is the equivalent to an EventEmitter, and the only way of multicasting a value or event to multiple Observers.

* **Schedulers: **are centralized dispatchers to control concurrency, allowing us to coordinate when computation happens on e.g. `setTimeout` or `requestAnimationFrame` or others.

#### Stream concept

An **observable** is just a **wrapper around a stream of values**, we can have one value or we have multiple values. Whatever the case we have our observer with the 3 methods mentioned before were we can handle any values

At the end we **might have and endpoint** when the observable is done. Sometimes this could never occur \(case a a click stream\), or  if we do complete the observable \(if we have some data source which eventually finishes then we can call end and we will execute complete if the observable provides it on the observer object.

![](/assets/Screen Shot 2017-07-12 at 15.26.51.png)If its the case of s stream or observable wrapping an HTTP request we **might ge**t a response that could be **an error** \(either a time out or a server-side error\)

The observable would through the error and we could handle it in the error function of the observer

![](/assets/Screen Shot 2017-07-12 at 15.41.19.png)

