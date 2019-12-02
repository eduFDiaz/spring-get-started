# Spring microservices getting started
Create an arch maven project and add the next to pom.xml
```
<parent>
  	<groupId>org.springframework.boot</groupId>
  	<artifactId>spring-boot-starter-parent</artifactId>
  	<version>1.4.2.RELEASE</version>
  </parent>
  
  <dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
  		<artifactId>spring-boot-starter-web</artifactId>
  	</dependency>
  </dependencies>
  
  <properties>
  	<java.version>1.8</java.version>
  </properties>
```
Decorate your main class
```
package com.codingindfw.springbootstarter;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CourseApiApp {
	
	public static void main(String[] args) {
		SpringApplication.run(CourseApiApp.class, args);
		System.out.println("Hello");
	}

}
```
And voila, your sprin app will be running on port 8080 😀

Now, you need to create a class and decorate it as a rest controller, see next:

```
package com.codingindfw.springbootstarter.hello;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

	@RequestMapping("/hello")
	public String sayHi() {
		return "Hello";
	}
}
```

Click on [localhost:8080/hello](https://localhost:8080/hello) to see the magic happening.