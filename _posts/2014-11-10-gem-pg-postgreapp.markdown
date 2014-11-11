---
layout: post
title:  "Instalando a gem pg com o PostgresApp"
date:   2014-11-10 17:50:30
categories: gem postgres pg postgresapp
---
Depois de muito quebrar a cabeça para instalar a gem do PG e usar o PostgresApp, achei a solução. Bastou rodar o comando abaixo no terminal:

{% highlight bash %}
$ sudo env ARCHFLAGS="-arch x86_64" gem install pg -- --with-pg-config=/Applications/Postgres.app/Contents/Versions/9.3/bin/pg_config
{% endhighlight %}
