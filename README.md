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

![alt](images/browser-hello.jpg)

create a topic class as it follows:
```
package com.codingindfw.springbootstarter.topic;

public class Topic {
	private int id;
	private String name;
	private String description;
	
	public Topic() {
	}
	
	public Topic(int id, String name, String description) {
		super();
		this.id = id;
		this.name = name;
		this.description = description;
	}
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getDescription() {
		return description;
	}
	public void setDescription(String description) {
		this.description = description;
	}
}
```
modify the getAllTopics() method in the controller:

```
@RequestMapping("/topics")
	public List<Topic> getAllTopics() {
		
		return Arrays.asList(
				new Topic(1, "java", "intro to java"),
				new Topic(2, "spring", "intro to spring"),
				new Topic(3, "asp", "intro to asp.net"),
				new Topic(4, "swagger", "intro to swagger")
				);
	}
```
visit the url and spring again does the magic for you:

![alt](images/topic-controller-Get-all-topics.jpg)

## Creating a service

Create a service and move the list of topics to it
```
package com.codingindfw.springbootstarter.topic;

import java.util.Arrays;
import java.util.List;

import org.springframework.stereotype.Service;

@Service
public class TopicService {
	private List<Topic> topics = Arrays.asList(
			new Topic(1, "java", "intro to java"),
			new Topic(2, "spring", "intro to spring"),
			new Topic(3, "asp", "intro to asp.net"),
			new Topic(4, "swagger", "intro to swagger")
		);
	
	public List<Topic> getAllTopics(){
		return this.topics;
	} 
}

```
Then spring will inject the server into our controller if we rewrite the controller as it follows:
```
package com.codingindfw.springbootstarter.topic;

import java.util.Arrays;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TopicController {
	
	@Autowired
	private TopicService topicService;
	
	@RequestMapping("/topics")
	public List<Topic> getAllTopics() {
		
		return topicService.getAllTopics(); 
	}
}

```

The output when visiting the url will be the same

![alt](images/topic-controller-Get-all-topics.jpg)