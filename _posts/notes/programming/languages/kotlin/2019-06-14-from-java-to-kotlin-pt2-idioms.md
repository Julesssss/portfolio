---
layout: post
title: From Java to Kotlin (2/2) - Idioms
date:   2019-06-16 11:57:00 +0100
categories: programming jvm kotlin
permalink: /notes/languages/kotlin/from-java-to-kotlin-idioms
---
Kotlin's has built-in support for common java patterns. This are some of them.

#### Create POJOs (Plain Old Java Object)  
This provides the class with `getters` (and `setters` for `vars`) as also `.toString()`,
 `equals()`, `copy()` etc.
~~~
data class Person(val name: String, var age: Int)
~~~

#### Params with default values  
It's possible to give default values to parameters
~~~ java
fun default(arg1: Int = 0, arg2: String = "oh no") {
  // whatever
}
~~~
<!--more-->
#### Filter a list
~~~ java
fun filterPositives() {
  val list = listOf(-2, -1, 0, 1, 2)
  val positives = list.filter(x -> x > 0)
}
~~~

#### Check is class instanceOf()  
~~~ java
fun isInstanceOf(obj: Any) {
    when(obj) {
        is String -> "str"
        is Integer -> "int"
        else -> "whatever"
    }
}
~~~

#### Ranges usage
~~~
fun ranges(value: Int) {

    // includes 10
    for(i in 1..10) {}

    // does not include 10  
    for(i in 1 until 10) {}

    // goes in steps of i+=2
    for (i in 2..10 step 2) {}

    // from 10 to 1, both included
    for (i in 10 downTo 1) {}

    if(value in 1..10) {}

}
~~~

#### Lazy property
~~~ java
val p: String by lazy {
    "compute the String here"
}
~~~

#### Execute if not null / else
~~~ java
fun executeIfNotNull(str: String?) {
    str?.let {
        println("is not null!")
    }
}

fun ifNotNullElse() {
    val files = File("test").listFiles()
    println(files?.size ?: "empty")
}
~~~

#### Get first item of possibly empty collection
~~~ java
fun getFirstItem() {
    val emails = emptyList<String>()
    val mainEmail = emails.firstOrNull() ?: ""
}
~~~

#### Consume a nullable Boolean
~~~ java
val b: Boolean? = ...
if(b == true) {

} else {
  // b is false or null
}
~~~

### Reference(s)
[https://kotlinlang.org/docs/reference/idioms.html](https://kotlinlang.org/docs/reference/idioms.html)
