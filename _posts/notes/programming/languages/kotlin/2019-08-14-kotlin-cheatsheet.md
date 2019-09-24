---
layout: post
title: Kotlin experience cheat-sheet
date:   2019-08-14 10:27:00 +0100
categories: [programming, kotlin]
permalink: /notes/languages/kotlin
---
## Mutable vs Inmutable collections
Kotlin's `List` from the standard library is readonly. This means if we use collections from Java Libraries such as Spring Data / JPA, the `List` we are going to get back is not the same as a Kotlin `List` but a `MutableIterable<>` interface.
This is an example on how to mock and inject a Java `List` in a Kotlin test.  
~~~ java
val courses = mutableListOf<Course>()
every { dao.findAll() } returns courses
~~~

## Spring Dependency Injection
This is the equivalent to constructor DI with `@Autowired` for the bean `Service` into `RestResource`
~~~ java
class RestResource(private val service: Service) {
  // whatever
}
~~~

<!--more-->

## Bean with automatically given ID
Example of a bean with an automatically given ID by Hibernate, primary and secondary constructors
~~~ java
@Entity
@Table(name = "course")
class Course(
        @Id
        @GeneratedValue(
        strategy = GenerationType.IDENTITY)
        val id: Long? = null,
        var username: String,
        var description: String) {

    constructor() :
            this(username = "",
            description = "")

    constructor(username: String,
                description: String) :
            this(null,
            username = username,
            description = description)
}
~~~

## Testing  
It's possible to use the same libraries and dependencies as with Java to transition slowly into Kotlin's style. It uses _JUnit 5_. Also _MockK_ instead of _Mockito_

Kotlin has it's own testing dependency to add to the pom.
~~~ xml
<dependency>
    <groupId>org.jetbrains.kotlin</groupId>
    <artifactId>kotlin-test</artifactId>
    <version>check_last_version</version>
    <scope>test</scope>
</dependency>
~~~

### Test template
~~~ java
@ExtendWith(MockKExtension::class)
internal class RestResourceTest {

  @MockK
  lateinit var service: Service

  @InjectMockKs
  lateinit var resource: Resource

  @Test
  internal fun testXXX() {
    // Given

    // When  

    // Then  

  }

}
~~~

#### Mocking
Same as `BDDMockito.given(personDao.findOne(id)).willReturn(person)`
~~~ java
val id = 123L
val person = Person()  
every { personDao.findOne(id) } returns person
~~~

#### Verify method
Same as `BDDMockito.verify(personDao).findOne(id)`
~~~ java
verify { personDao.findOne(id) }
~~~

#### Assert Exception
This needs the artifact _kotlin-test_ at the _POM_.
~~~ java
assertFailsWith<Exception>("message") {
  this.restResource.getCourse(id)
}
~~~
