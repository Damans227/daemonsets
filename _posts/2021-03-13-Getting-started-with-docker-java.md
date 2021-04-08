---
layout: single
title:  "Getting started with Docker-Java"
date:   2021-03-13 12:49:11 -0500
categories: Docker
show_date: true 
header:
  image: /assets/images/Docker-Java.webp
tags: docker java
---

In this article, we take a look at a `Java API Client for Docker`.
Throughout the article, I am going to articulate the way of how to connect with a running Docker Daemon and what type of important functionality the API offers to Java developers.

<h1 id="Overview">1. Overview</h1>

I have been using docker for containerizing my apps for a while now. As an inherent developer, I have had this urge to develop a custom Docker Client to simplify and streamline the process of containerization. So, recently I decided to take up a personal project and develop an end to end application with an intuitive graphical user interface (GUI) that can connect with Docker Daemon on the backend and execute Docker CLI commands based on the user input received via a centralized Dashboard.

<blockquote>
Although, I am still working on this app, but when I was exploring the Docker-Java API available out there, I ended up writing a simple JAVA utility that can deploy a container for you in just few clicks. Lemme walk you through this journey of mine. 
</blockquote>

<h1 id="Getting-started">2. Getting Started</h1>

Docker offers an API to interact with the Docker Daemon (called the Docker Engine API) and official SDK libraries written in Go and Python. Since, I have knack for JAVA, I will be using an unofficial Java API client for Docker, called docker-java. 

<h1 id="Maven-dependency">3. Maven Dependency</h1>

First, we need to add the main dependency into our `pom.xml` file:

{% highlight xml %}
<!-- https://mvnrepository.com/artifact/com.github.docker-java/docker-java -->
<dependency>
        <groupId>com.github.docker-java</groupId>
        <artifactId>docker-java</artifactId>
        <version>3.0.14</version>
</dependency>
{% endhighlight %}

<h1 id="Docker-client">4. Using a Docker Client</h1>

In order to communicate with `Docker Daemon`, we have to instantiate a Docker Client by leveraging DockerClient java interface which relies on a builder class called `DockerClientConfig`. `DockerClientConfig` is used for telling the library how to access Docker, which credentials to use to pull from Docker registries, etc etc. 

{% highlight java %}
DefaultDockerClientConfig clientConfig = DefaultDockerClientConfig.createDefaultConfigBuilder()
    		.withDockerHost("tcp://127.0.0.1:2375")
    		.withDockerTlsVerify(false)
    		.build();
    	
DockerClient dockerClient = DockerClientBuilder.getInstance(clientConfig).build();
 {% endhighlight %}

<h1 id="Container-management">5. Container Management</h1>

<h2 id="Pull-an-image">5.1 Pull An Image </h2>

To download images from registry services, we make use of the `pullImageCmd()` method.

{% highlight java %}
Scanner in = new Scanner(System.in);
System.out.println("Enter the name of an image to be pulled: ");
String pullImage = in.nextLine();

dockerClient.pullImageCmd(pullImage).withTag("latest").exec(new PullImageResultCallback()).awaitCompletion();
{% endhighlight %}

<h2 id="Creat-a-new-container">5.2 Create new container </h2>

Creating a container is served with the `createContainerCmd()` method as shown below:

{% highlight java %}
 CreateContainerResponse newContainer1 =
                dockerClient
                    .createContainerCmd(pullImage)
                    .withTty(false)
                    .withStdinOpen(true)
                    .exec();
 {% endhighlight %}

<h2 id="Start-a-container">5.3 Start a container</h2>

Once we create the container, we can start it by name or id respectively:

{% highlight java %}
dockerClient.startContainerCmd(newContainer1.getId()).exec();
{% endhighlight %}

<h2 id="Container-inspection" >5.4 Container inspection</h2>

The `inspectContainerCmd()` method takes a String argument which indicates the name or id of a container. Using this method, we can observe the metadata of a container directly:

{% highlight java %}
InspectContainerResponse inspectContainer1 
    	  = dockerClient.inspectContainerCmd(newContainer1.getId()).exec();
    	
    	System.out.println("Inspection Details: "+inspectContainer1.getId()+"  "+inspectContainer1.getState().getStatus())
 {% endhighlight %}


<h2 id="Listing-containers">5.5 Listing containers</h2>

Now, we can list all the running containers located on the Docker host. `listContainersCmd()` will return a list object, which you can iterate through as shown below: 

{% highlight java %}
List<Container> containers = dockerClient.listContainersCmd().withShowAll(true).exec();
    	
Iterator<Container> it = containers.iterator();
    	
while(it.hasNext()) {
    		
    Container container = it.next();
    System.out.println(container.getImage()+"  "+container.getStatus());

}
{% endhighlight %}


<h2 id="Stop-a-container">5.6 Stop a container </h2>

You can stop the newly created container by using method, `stopContainerCmd()`. 

{% highlight java %}
while(true) {
    		
    System.out.println("\nEnter 'Y' to stop the container:");
    String ans = in.nextLine();
    	
    if(ans.equals("Y")) {
    		
    	dockerClient.stopContainerCmd(newContainer1.getId()).exec();
    		break;
    }
    }
System.out.println("Container for "+pullImage+ " stopped!");
{% endhighlight %}

<h1 id="Summary">6. Summary</h1>

This article provides you with a very brief introduction to `Docker-Java api` for creating custom apps to manage docker. The app I have created is available on my [Github][Github-repo]. You can clone the repo and give it a try. 

[Github-repo]: https://github.com/Damans227/docker-java