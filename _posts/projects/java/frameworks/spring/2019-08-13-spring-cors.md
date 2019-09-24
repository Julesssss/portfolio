---
layout: post
title: Spring CORS
date:   2019-08-13 13:40:00 +0100
categories: programming java kotlin frameworks spring cors
permalink: /notes/frameworks/java/spring/cors
---
## CORS (Cross-Origin Resource Sharing)
It's a mechanism to let a web application running at one domain, protocol or port have permission to access resources from a server at a different one.  

This is needed if you have, for example, a Frontend running on port :3000 (React) consuming a Backend API running on port :34831 (custom port for Spring). Unless CORS are set, FE will not be able to access BE resources.

## In Spring  
It's possible to enable them for a single `RestResource` or globally for the whole application.  

_(This example has been done in Kotlin)_

### By RestResource  
~~~ java
@RestController
@RequestMapping("courses")
@CrossOrigin("http://localhost:3000")
class CourseRestResource {
  // dependencies and methods
}
~~~

<!--more-->

### Globally  
This is done at a `SpringConfig` level, creating a new `@Bean` as follows.

~~~ java
@Configuration
@ComponentScan(basePackages = ["redacted"])
class SpringConfig {

  @Bean
  fun corsFilter(): CorsFilter {
    val origin = "http://localhost:3000"
    val headers = listOf("Origin", "Content-Type", "Accept")
    val methods = listOf("GET", "POST", "PUT", "OPTIONS", "DELETE")
    val source = UrlBasedCorsConfigurationSource()
    val config = CorsConfiguration()
    config.allowCredentials = true
    config.allowedOrigins = Collections.singletonList(origin)
    config.allowedHeaders = headers
    config.allowedMethods = methods
    source.registerCorsConfiguration("/**", config)
    return CorsFilter(source)
  }

}
~~~

## Resource(s)
[https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  
[https://stackoverflow.com/questions/51720552/enabling-cors-globally-in-spring-boot](https://stackoverflow.com/questions/51720552/enabling-cors-globally-in-spring-boot)
