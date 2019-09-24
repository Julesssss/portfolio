---
layout: post
title: From Java to Kotlin (1/2) - Basic Syntax
date:   2019-06-14 13:57:00 +0100
categories: programming jvm kotlin
permalink: /notes/languages/kotlin/from-java-to-kotlin-basic-syntax
---
Guide on differences to jump from Java developer to Kotlin developer.  

#### Class instantiation
No `new` operator is needed
~~~ java
  class Whatever {
      fun createClass() {
        val person = Person()
      }    
  }
~~~
<!--more-->
#### Function declaration
Two `Int` parameters and an `Int` return value
~~~ java
fun sum(arg1: Int, arg2: Int): Int {
  return arg1 + arg2
}
~~~

The return value may be inferred and the function used as an expression
~~~ java
fun sum(arg1: Int, arg2: Int) = arg1 + arg2
~~~

#### Variables
There're 2 types of variables `val` and `var`. The first is a read-only variable and the former may be re-assigned.
~~~ java
fun variables() {
  val readOnly: Int = 1 // type assigned on declaration
  var normalVariable = 2 // type inferred
}
~~~

#### String templates
Strings are more powerful than on Java
~~~ java
var a = 1
val string1 = "a is $a"
// would print "a is 1"

a = 2
val string2 = "${string1. replace("is, "was)}, but now is $a"
// would print "a was 1, but now is 2"
~~~

#### Null Safety
Kotlin differences between nullable and non-nullable references
~~~ java
var nonNullable: String = "Hello world"
nonNullable = null // compilation error

var nullable: String? = "Hello world"
nullable = null // okay
~~~

For more information about this, search for my _Kotlin - null safety_ post.

#### 'Is' operator
Checks the type of a variable
~~~ java
if (obj !is String)
  return null
else
  return obj.length // automatic cast to string
~~~

### Expressions
#### 'When' expression
Is similar to Java's switch
~~~ java
fun whenExpression(obj: Any): String =
  when(obj) {
    1 -> "one"
    "hello" -> "greeting"
    is Long -> "Long"
    else -> "anything"
  }
~~~

#### Conditional expressions
Just as methods, conditionals may be used as expressions
~~~ java
fun cond(a: Int, b: Int) = if(a > b) a else b
~~~

#### 'If' expression
~~~ java
fun ifExpression(arg1: Int) {
    val result = if(arg1 == 1) {
        "one"
    } else if(arg1 == 2) {
        "two"
    } else {
        "three"
    }
}
~~~

#### 'Try/catch' expression
~~~ java
fun tryCatchExpression(arg1: Int) {
    val result = try {
        arg1 / 0
    } catch (ex: ArithmeticException) {
        throw IllegalStateException(ex)
    }
}
~~~

### Reference(s)
[https://kotlinlang.org/docs/reference/basic-syntax.html](https://kotlinlang.org/docs/reference/basic-syntax.html)
