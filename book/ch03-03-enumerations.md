# Enumerations

Flix supports enumerations (also known as [algebraic data types](https://en.wikipedia.org/wiki/Algebraic_data_type), 
sum types or tagged unions).

An enumeration is declared with the `enum` keyword:

```flix
enum Color {
    case Red,
    case Green,
    case Blue
}
```

We refer to the members of this enumeration as `Color.Red`, `Color.Green` and `Color.Blue`.

For example, we can write:

```flix
def r: Color = Color.Red
def g: Color = Color.Green
def b: Color = Color.Blue
```

We can check if a value of type `Color` is `Color.Red` with an equality test:

```flix
def f(c: Color): Int = 
  if (c == Color.Red) 
    ... 
  else 
    ...
```

However, the preferred style is to use pattern matching:

```flix
def f(c: Color): Int = match c with {
    case Color.Red => ...
    case Color.Green => ...
    case Color.Blue => ...
}
```

Enumerations can be nested and hold other types:

```flix
enum Shape {
    case Circle(Int, Color),
    case Square(Int, Color),
    case Rectangle(Int, Int, Color) 
}
```

We can create values of this type:

```flix
def sq: Shape = Shape.Square(42, Color.Red)
```

and destruct them with pattern matching:

```flix
def f(s: Shape): Color = match s with {
    case Shape.Circle(_, c) => c
    case Shape.Square(_, c) => c
    case Shape.Rectangle(h, w, c) => c
}
```

