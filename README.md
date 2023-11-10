# any_vs_some

Sure, let's illustrate the difference between `any` and `some` with practical examples.

**Using `any`**:
Suppose you have a protocol called `Shape` representing geometric shapes. You want to create an array that can hold instances of different types that conform to the `Shape` protocol, like circles, rectangles, and triangles.

```swift
protocol Shape {
    func area() -> Double
}

struct Circle: Shape {
    var radius: Double
    
    func area() -> Double {
        return Double.pi * radius * radius
    }
}

struct Rectangle: Shape {
    var width: Double
    var height: Double
    
    func area() -> Double {
        return width * height
    }
}

let shapes: [any Shape] = [Circle(radius: 5.0), Rectangle(width: 3.0, height: 4.0)]

for shape in shapes {
    print("Area: \(shape.area())")
}
```

In this example, we define an array `shapes` of type `[any Shape]`. It means that this array can hold any value conforming to the `Shape` protocol. We can store both `Circle` and `Rectangle` instances in this array.

**Using `some`**:
Now, let's consider a situation where we want to define a function that returns an instance of a specific type conforming to the `Shape` protocol. However, we want the exact type to be determined by the implementation, and we don't want to expose the concrete type to the caller.

```swift
func createShape(isCircle: Bool) -> some Shape {
    if isCircle {
        return Circle(radius: 3.0)
    } else {
        return Rectangle(width: 2.0, height: 4.0)
    }
}

let myShape = createShape(isCircle: true)
print("Area: \(myShape.area())")
```

In this example, the `createShape` function returns an instance of `Shape` without specifying the concrete type. The `some Shape` return type indicates that the returned value conforms to the `Shape` protocol, but the exact type (whether it's a `Circle` or `Rectangle`) is determined by the function's implementation. 

In both cases, `any` and `some` are used to abstract the concrete types, but `any` is used when defining a variable or array that can hold any value conforming to a protocol, while `some` is used when defining a return type that abstracts the concrete type and allows it to be determined by the implementation.
