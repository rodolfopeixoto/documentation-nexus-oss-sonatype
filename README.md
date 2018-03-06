# NEXUS OSS

Nexus

Versão do Projeto OSS 2.14.8-01
=========================================================

ATENÇÃO
================================

**Username:** admin
**Password:** admin123


Configuração inicial
================================

O docker-compose está configurado para rodar na porta **8081**. Para acessar o sistema você deve utilizar:
localhost:8081.

Documentação
----------------------

Para rodar o nexus basta:

```
docker-compose up
```

Acessar o sistema: localhost:8081/nexus


Para criar um repostitório para uma determinada linguagem, devemos seguir os passos abaixo:

**1** - Clique no botão **+ Add**

**2** - **Proxy Repository**

**3** - **Repository ID** ( dê o nome que desejar, porém ele será o ID único: rubygems)

**4** - **Repository Name**: ( dê um nome a esse repostirorio RubyGems)

**5** - Em **Remote Storage Location** adicione o endereço do repositório. Por exemplo: https://rubygems.org/

**6** - Clique em **Save**.

Caso, você tenha **PROXY**, vamos configurar:

Clique em **Administration** ( Aba à esquerda ) e clique em **Server**.

Em baixo, você verificará uma caixa para marcar escrito: **Default HTTP Proxy Settings (optional)** e **Default HTTPS Proxy Settings (optional defaults to HTTP Proxy Settings)**:

Em ambos marque e adicione o **Proxy Host** e a **Porta**, após adicionar, basta clicar em save.

Depois volte ao link **Repositories** com o botão direito no repositório que você criou, clique em **Allow Proxy**


Agora você pode configurar seu projeto:

É necessário adicionar as configurações abaixo para que funcione o sistema para ruby gems ou bundle.

**DOCKERFILE**

```
RUN gem sources --add http://admin:admin123@10.0.18.65:8081/nexus/content/repositories/rubygems-org/
RUN gem sources --remove https://rubygems.org/
RUN gem sources -c
RUN gem sources
RUN bundle config mirror.http://rubygems.org http://admin:admin123@10.0.18.65:8081/nexus/content/repositories/rubygems-org/
RUN bundle config
```

Link para configurar o proxy para outras linguagens:
[PROXY](https://books.sonatype.com/mcookbook/reference/repoman-sect-proxy-repo.html)

### Links diretos

Desenvolvimento
---------------------
-   [Rodolfo Peixoto](http://www.rodolfopeixoto.com.br)
