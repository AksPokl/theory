Null safety

class Cat(val age: Int, val name: String)

fun main() {
val cat = null
function(cat) // null 
}
? - it's possible to place null

fun function(cat:Cat?){
    print(cat?.age)
}

Unit object corresponds to the void type in Java.

use вместо try with resources

open class Any - The root of the Kotlin class hierarchy. Every Kotlin class has Any as a superclass.

Nothing has no instances. You can use Nothing to represent "a value that never exists": for example, if a function has the return type of Nothing, it means that it never returns (always throws an exception).


