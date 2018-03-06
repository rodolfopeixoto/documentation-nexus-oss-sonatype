# NEXUS OSS

Nexus

Versão do Projeto 0.1
================

Sobre esta versão
---------------------

Site desenvolvido:

Utilizado:

ATENÇÃO
---------------------

Configuração inicial
---------------------

DOCKERFILE

```
# FROM ruby:2.3 
# RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs 
# # for capybara-webkit 
# RUN apt-get install -y libqt4-webkit libqt4-dev xvfb 
# RUN sudo apt-get upgrade -y 
# RUN sudo mkdir /codemca 
# WORKDIR /codemca 
# ADD Gemfile /codemca/Gemfile 
# ADD Gemfile.lock /codemca/Gemfile.lock 
# # RUN sudo gem uninstall -i /usr/local/lib/ruby/gems/2.3.0 bundler 
# RUN gem install bundler -v 1.16.0.pre.3 --pre 
# # RUN bundle update smart_listing 
# # RUN gem install rdoc -v '4.3.0' 
# RUN  bundle install --binstubs --path vendor/bundle 
# ADD . /codemca 
# # RUN gem install rake 
# # RUN bundle exec rake namespace:start 
# RUN rake -v 
FROM ruby:2.3.1 
ENV http_proxy "http://10.131.188.1:80" 
ENV https_proxy "http://10.131.188.1:80" 
RUN apt-get update -yqq \ 
  && apt-get install -yqq --no-install-recommends \ 
    postgresql-client \ 
    nodejs \ 
    qt5-default \
    xvfb \
    libqt5webkit5-dev  \
    gstreamer1.0-plugins-base \
    gstreamer1.0-tools \
    gstreamer1.0-x \
    iceweasel \
  && apt-get -q clean

RUN apt-get install -y aptitude
RUN aptitude install -y graphviz

WORKDIR /codemca
COPY Gemfile* ./
RUN gem sources --add http://admin:admin123@10.0.18.65:8081/nexus/content/repositories/rubygems-org/
RUN gem sources --remove https://rubygems.org/
RUN gem sources -c
RUN gem sources
RUN gem install capybara-webkit
RUN bundle config mirror.http://rubygems.org http://admin:admin123@10.0.18.65:8081/nexus/content/repositories/rubygems-org/
RUN bundle config
RUN bundle install 
COPY . . 

```

Link para configurar o proxy:
[PROXY](https://books.sonatype.com/mcookbook/reference/repoman-sect-proxy-repo.html)

O docker-compose está configurado para rodar na porta **8081**, caso tenha interesse em modificar, basta ir ao 

Documentação
----------------------

Para rodar o nexus basta:

```
docker-compose up
```

Acessar o sistema: localhost:8081/nexus

### Links diretos

Desenvolvimento
---------------------
-   [Rodolfo Peixoto](http://www.rogpe.me)
