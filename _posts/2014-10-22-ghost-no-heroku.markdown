---
layout: post
title:  "Como fazer deploy do Ghost no Heroku"
date:   2014-10-22 22:50:30
categories: ghost heroku
---
Deu um certo trabalho fazer o deploy de uma aplicação Ghost para o Heroku. Oficialmente, não há suporte. :(

É um pouco tricky, mas nada demais.

* Instalar [Node.JS][node].
* Download do [Ghost][download-ghost].
* Inicie a aplicação:

{% highlight bash %}
$ npm install –production
$ npm start
{% endhighlight %}

* Acesse [http://127.0.0.1:2368][localhost] para verificar se o servidor está rodando. Se tudo estiver OK, acesse [http://127.0.0.1:2368/ghost/][localhost-ghost] e faça seu cadastro.
* Crie uma nova aplicação no Heroku.
* Acesse [https://addons.heroku.com/heroku-postgresql][heroku-postgresql] e adicione o Postgres na sua aplicação.
* Acesse [https://postgres.heroku.com/databases/][heroku-databases] e depois o banco da sua aplicação.
* Abra o arquivo `config.js` e altere as configurações do banco de produção (trocando <...> pelas configurações do Heroku):

{% highlight json %}
production: {
  url: '<URL_DA_APLICACAO>',
    mail: {},
    database: {
      client: 'postgres',
        connection: {
        host: '<HOST>',
        user: '<USER>',
        password: '<PASSWORD>',
        database: '<DATABASE>',
        port: '5432'
      },
      debug: false,
      filestorage: false
    },
    server: {
      host: '0.0.0.0',
      port: process.env.PORT
    }
},
{% endhighlight %}

* Adicione `"pg": "latest"` nas dependências no arquivo package.json
* Crie um arquivo `Procfile` na raiz do projeto com o seguinte conteúdo:
{% highlight text %}
web: NODE_ENV=production node index.js
{% endhighlight %}

* Iniciar o repositório git, adicionar Heroku como remote e etc...

{% highlight bash %}
$ git init
$ git remote add heroku git@heroku.com:<NOME_DA_APP>.git
$ git add . -A
$ git commit -m "Initial commit"
$ git push heroku master
{% endhighlight %}

* E isso deve funcionar. :)

[node]:           http://www.nodejs.org/
[download-ghost]:    https://ghost.org/download/
[jekyll-help]: https://github.com/jekyll/jekyll-help
[localhost]: http://127.0.0.1:2368
[localhost-ghost]: http://127.0.0.1:2368/ghost/
[heroku-postgresql]: https://addons.heroku.com/heroku-postgresql
[heroku-databases]: https://postgres.heroku.com/databases/
