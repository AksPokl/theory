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

