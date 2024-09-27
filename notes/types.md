


## Width
Width with a `2.W` constructor

## Bit

```scala
val a = Bool()
``` 

## Unsigned Integer

```scala
val a = UInt(2.W)
```

## Signed Integer

Is still just a bitvector, but allows for negative integer literals.

```scala
val a = SInt(2.W)
```

## Aggregate

```scala
val a = Vec(2, UInt(2.W))
```

## Bundle

```scala
class MyBundle extends Bundle {
  val a = UInt(2.W)
  val b = Bool()
}
```

# Random

```scala
val a = rand(UInt(2.W)) // -> rand logic [1:0] a;
val b = rand(Vec(2, UInt(2.W))) // -> rand logic [1:0] b[1:0];
val c = rand(Bool()) // -> rand logic c;
val d = rand(new MyBundle) // -> rand logic [1:0] d_a; rand logic d_b;
```

Potentially, extensions for scala data types could be added, but this is not a priority.

```scala
val e = rand(Int) // -> rand integer e;
val f = rand(String) // -> rand string f;
val g = rand(Double) // -> rand real g;
```




## AST

```scala
case class Width(width: Int)
case class BitVector(width: Width)
case class UInt extends BitVector
case class SInt extends BitVector
case class Aggregate(width: Width, tpe: Type)
case class Bundle(fields: Seq[(String, Type)])