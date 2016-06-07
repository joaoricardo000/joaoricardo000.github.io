---
layout:     post
title:      "API Blueprint"
subtitle:   "Documentation with benefits"
date:       2015-06-03 12:00:00
author:     "joaoricardo000"
header-img: "img/4.jpg"
---

Every now and then, during any stage of an application development, you have to know which are and how to use some API endpoints. 

API Blueprint solves this in a collaborative way, and does a bunch more.  
  
## What is it?  
  
The short answer is "documentation with benefits".  
From the [official website](https://apiblueprint.org/):  

>API Blueprint. A powerful high-level API description language for web APIs.  
>API Blueprint is simple and accessible to everybody involved in the API lifecycle. Its syntax is concise yet expressive. With API Blueprint you can quickly design and prototype APIs to be created or document and test already deployed mission-critical APIs.


  
A blueprint is a markdown text following some rules to summarize an API.  
For example:  
  
```markdown 

# GET /message
+ Response 200 (text/plain)

        Hello World!  

```

That tells you that a **GET** in **/message** returns a 200 HTTP code and 'Hello World!' in *text/plain* format. 
  
  
Besides the endpoints, you can also map every object that flows in the API as easy as:  
  
```markdown   	

# Data Structures

## BlogPost (object)
+ id: 42 (number, required)
+ title: A blog post!
+ text: Hello World
+ author (Author) - Author of the blog post.

## Author (object)
+ name: Boba Fett
+ email: fett@intergalactic.com

```


Of course there is a bunch more of parameters that you can use to describe a real world API.  
A more complete example, using the objects above, looks like this:

```markdown   	
  
{% include blog/apiblueprint/example.md %}

```

  
In this example we can see that a HTTP **GET** in **/posts** work as a filter endpoint, and which are the query parameters available with default values.  
So a GET in ```http://api-base-url/posts?author_name=Fett```, will return something like this:  

```json
[{
	"id":42,
	"title":"A blog post",
	"test":"Hello world",
	"author":{
		"name":"Boba Fett",
		"email":"fett@intergalactic.com"
	}
}]
```

On the same endpoint, a **POST** will create a new blog post. It requires a specific HTTP header, *access_token*, and a JSON body with title and text keys.  
  
With this information you can already start to build a client for this API.

You can check API Blueprint examples in their [official github repository](https://github.com/apiaryio/api-blueprint/tree/master/examples).
  
## Beautifull output!  
  
You can render the above markdown to html, just like this blog post (using jekyll). It looks like this:

---
---

{% include blog/apiblueprint/example.md %}

---
---
  
You can also use a [very cool renderer called aglio](https://github.com/danielgtaylor/aglio)
![](/img/blog/apiblueprint/aglio.jpeg)
![](/img/blog/apiblueprint/aglio2.jpeg)
Seriously, how many times you wished that API you are working with had this nice documentation.
Easy to read for everyone.  


## The benefits!  
  
It is not only a beautiful pattern for documentation!  

As you might be wondering, it can be executed somehow.  
Using [api-mock](https://github.com/localmed/api-mock) you can start a HTTP server as simple as:  
```  
$ api-mock your-blueprint.md
```  
You can use this mocked API to build your application frontend, isolated from the backend environment. You can also define a delivery for a freelance API. 
  
You can create tests from it, and manage the backend development status by how many endpoints are working or not. If you have a big undocumented API, there are tools to create a blueprint from HTTP requests.  
  
There are services, like [Apiary](https://apiary.io/), that let you host a blueprint file and mocks a server in the cloud. Very useful to share documentation and a mocked server between everyone involved in the project.  

[Check all official supported tools for API Blueprint](https://apiblueprint.org/tools.html).


## Why you should use it?  

It is easy, fast, simple and solves real problems.  
  
Knowing every part of an API by heart is really hard and you should leave room in your head for more important things. With a couple hours, from no experience to a complete API Blueprint, you can solve that problem for you and everyone else.  

When starting a fresh new project, API blueprint is also really helpful. You can sit down with all parts involved in the development and define objects, parameters, endpoints and interactions needed for a complete application. And everyone can edit it later when needed.  

You can create a frontend development environment, using a mocked server, to quickly integrate with production just changing an *api-baseurl* configuration.
  
If you are working with a team, you can split work and integrate parts based on the blueprint. If you are working alone, helps you not lose your mind.  

## API Blueprint alternatives

There are a few of others modeling api tools available.  

[RAML (RESTful API Modeling Language)](http://raml.org/) uses YAML, you can import parts from another files, works with authentication and is also quite easy to write.

[Swagger](http://swagger.io/) is the most popular right now. You write using JSON. It is not so easy to get started, but it is a very powerful tool. You can even generate code in many languages from the documentation.  
  
The choice is a matter of taste. I like API Blueprint because it feels simple to me. But it is an opinion. You can [search](https://www.google.com.br/search?q=api+blueprint+vs+swagger+vs+raml) the web for more points of view and comparisons.

## Getting started

[apiblueprint.org](https://apiblueprint.org/documentation/tutorial.html) have a very good straightforward tutorial. A quick look will give you an idea of what you can do.