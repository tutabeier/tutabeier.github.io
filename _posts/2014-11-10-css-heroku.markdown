---
layout: post
title:  "Alterações em CSS não são aparecem no Heroku."
date:   2014-11-10 16:50:30
categories: css rails heroku
---
Modifiquei um CSS e tudo funcionou muito bem localmente, mas não no Heroku.

Durante o push pro Heroku eu vi essa linha

{% highlight bash %}
Include "rails_12factor" gem to enable all platform features
{% endhighlight %}

Instalei a gem e as mudanças tiverem efeito.

{% highlight bash %}
$ gem 'rails_12factor'
{% endhighlight %}
