First, let's make a counter stream that indicates how many times a button was clicked. In common Reactive libraries, each stream has many functions attached to it, such as

`map`, `filter`, `scan`, etc. When you call one of these functions, such as `clickStream.map(f)`, it returns a **new stream **based on the click stream. It does not modify the original click stream in any way. This is a property called **immutability**, and it goes together with Reactive streams. That allows us to chain functions like `clickStream.map(f).scan(g)`

```
  clickStream: ---c----c--c----c------c-->
               vvvvv map(c becomes 1) vvvv
               ---1----1--1----1------1-->
               vvvvvvvvv scan(+) vvvvvvvvv
counterStream: ---1----2--3----4------5-->
```

The `map(f)` function replaces \(into the new stream\) each emitted value according to a function `f `you provide. In our case, we mapped to the number 1 on each click. The `scan(g) `function aggregates all previous values on the stream, producing value `x = g(accumulated, current) `, where `g `was simply the add function in this example. Then, `counterStream `emits the total number of clicks whenever a click happens.

