First, let's make a click stream that indicates how many times a button was clicked. In common Reactive libraries, each stream has many functions attached to it, such as

`map`, `filter`, `scan`, etc. When you call one of these functions, such as `clickStream.map(f)`, it returns a **new stream **based on the click stream. It does not modify the original click stream in any way. This is a property called **immutability**, and it goes together with Reactive streams. That allows us to chain functions like `clickStream.map(f).scan(g)`

```
  clickStream: ---c----c--c----c------c-->
               vvvvv scan(c becomes 1) vvvv
               ---1----1--1----1------1-->
               vvvvvvvvv scan(+) vvvvvvvvv
counterStream: ---1----2--3----4------5-->
```

The `map(f)` function replaces \(into the new stream\) each emitted value according to a function `f`you provide. In our case, we mapped to the number 1 on each click. The `scan(g)`function aggregates all previous values on the stream, producing value `x = g(accumulated, current)`, where `g`was simply the add function in this example. Then, `counterStream`emits the total number of clicks whenever a click happens.

#### Example

[jsbin](https://jsbin.com/rogevob/edit?html,js,console,output)

#### terminology

Rx    // package

Observable    // object

fromEvent\(source, type-of-event\)    // helper method that create a **new** observable based on an event.

scan\(\)    // The **scan **operator works just like **reduce **for arrays. It takes a value which is exposed to a callback. The returned value of the callback will then become the next value exposed the next time the callback runs. 



e.g.: if you have an array of numbers a reduce function could give you the total sum, while scan will give you each partial sum until the last that will be the same total as reduce result

**reduce**

```
var observable = Rx.Observable.of(1,2,3,4,5)

observable
    .reduce((total, currentValue) => {
        return total + currentValue;
    }, 0)
    .subscribe({
        next: function(value) {
            console.log(value);
        }
    });

// 15
```

**scan**

```
observable
    .scan((total, currentValue) => {
        return total + currentValue;
    }, 0)
    .subscribe({
        next: function(value) {
            console.log(value);
        }
    });

// 1, 3, 6, 10, 15
```

subscribe\( next-method, error-method, complete-method \)    // to react to that event I need to subscribe to it. 3 parameter functions.

--

"operators like scan allows you to transform the way this data is used or looks like immensely, helps you control how the events flow through your observables."

--

You can think about rxjs and observables as a funnel-like approach for handling asynchronous code

