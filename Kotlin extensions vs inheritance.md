Kotlin Extensions vs Inheritance
=====


we usually use inheritance in our code as it is **OOP** concept. we use this concept to extend classes and add feature or properties to the class.

There is another concept in new programming language like **Kotlin** called **extension** which can add functionality to class without extending it

Inheritance
----

Inheritance is nothing but extending a class and adding functionality to it. You can add properties (variables) as well as functions in the extending class. You can access the variables of extending ( ***Base*** ) class if they are not private ( ***protected or internal or public*** ) can override them if they are not final (open variables) or you can override the functions also

```
    open class MotorVehicle(val maxSpeed: Double, val horsePower: Int) {
        open fun getDetails(): String {
            return "$maxSpeed :: $horsePower"
        }
    }

    class Car(
        val color: String,
        maxSpeed: Double,
        horsePower: Int
    ) : MotorVehicle(maxSpeed, horsePower) {
        override fun getDetails(): String {
            return "$maxSpeed :: $horsePower :: $color"
        }
    }
```
and we can call it 
```
    var car = Car("RED", 200.50, 2000)
    println(car.getDetails())
```
> ## Inheritance Notes:
> - can add properties and override function of the base class (***non final class***)
> - you can access properties and functions from Base class

Extensions
---
adding function to a class without extending the class, and all objects of the class type will have this function.

```
class Car(val maxSpeed: Double)

fun Car.getDetails(): String {
    return "$maxSpeed"
}
```
and we can call it 
```
var car = Car(200.20)
println(car.getDetails())
```
> ## Extensions Notes:
> - can add funtion to a class and this class should not be (***non final class***)
> - extensions does not need extending base class
> ## Extensions Limitations:
> - can't access the protected variables/ functions of the class 
> - Can't add any new variable/properties in your extension functions

## how are extension functions resolved?
it is resolved statically 

example:
```
open class BaseClass()
class DerivedClass(): BaseClass()
fun BaseClass.doSomething() {
    print("BaseClass.doSomething")
}

fun DerivedClass.doSomething() {
    print("DerivedClass.doSomething")
}
```
to call it 
```
fun callFunction(base: BaseClass) {
    base.doSomething()
}

callFunction(DerivedClass())
```
> this callFunction wll print ```BaseClass.doSomething``` because the reference for this function from type base class not the derived and it is different than the inheritance which is resolved by runtime **Polymorphism**
