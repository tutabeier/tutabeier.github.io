---
layout: post
title:  "Using dynamic slaves on Jenkins"
date:   2017-02-14 23:26
categories: jenkins ci cd
---
One of the common scenarios I've face when using Jenkins is that usually the executors are idle and the combination of nodes and executors are underused.

It's also common to have different slaves with different configurations in order to serve to different needs. For example, right now I'm working for a client which has one team that supports the single Jenkins instance that is responsible for the whole organization's builds. The slaves have some flavors: Maven, NPM or Docker. If one team works with Gradle, for example, the team is responsible to configure the container which will build, run and publish the application.

So, in a in certain sense, the team does have some independency from the operations team.

So I've started asking me one question: is there any way to have dynamic slaves and optimize the operation's team, development teams and do not underuse the executors on a slave?

First of all, I've created this `docker-compose.yml` in order to spin up the master and slave easily:
{% highlight dockerfile %}
FROM jenkins:alpine
MAINTAINER Lucas Beier <lucas.beier@gmail.com>
USER root

RUN apk --update add docker
{% endhighlight %}

And then I built and started the container:
{% highlight bash%}
docker build -t jenkins-docker .
docker run -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 -p 50000:50000 -it --rm jenkins-docker
{% endhighlight %}

After that I've installed the [Docker Plugin][docker_plugin] and configured it:
![Docker plugin config](/img/jenkins_docker_plugin.png)


[docker_plugin]: https://wiki.jenkins-ci.org/display/JENKINS/Docker+Plugin
