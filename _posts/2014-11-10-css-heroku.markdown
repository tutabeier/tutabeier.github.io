---
layout: post
title:  "Alterações em CSS não são aparecem no Heroku."
date:   2014-11-10 16:50:30
categories: css rails heroku
---
Modifiquei um CSS e tudo funcionou muito bem localmente, mas não no Heroku. Fui atrás do problema e descobri que é preciso precompilar os assets e commitar as mudanças.

Dê um git status para verificar que não falta nada. Depois:

{% highlight bash %}
$ bundle exec rake tmp:clear
$ bundle exec rake assets:clean RAILS_ENV=production
$ bundle exec rake assets:precompile RAILS_ENV=production
$ git add .
$ git commit -m "<MENSAGEM_DE_COMMIT>"
$ git push heroku master
{% endhighlight %}
