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



