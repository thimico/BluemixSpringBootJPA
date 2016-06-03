<h1> IBM Bluemix - Spring Boot / Spring Data JPA / demo </h1>

O seguinte demonstração mostra como vincular uma aplicacao Spring Boot a um serviço MySQL [Spring Data JPA]. 
Isso garante que você não tem que escrever qualquer código para recuperar os detalhes da conexão de fonte de dados ligados como
spring auto configura isso para você usando Spring biblioteca de conectores de serviços em nuvem.

Você pode implantar esta aplicação automaticamente para sua conta Bluemix usando o botão abaixo, ou você pode seguir os passos abaixo.

<a href="https://bluemix.net/deploy?repository=https://github.com/thimico/BluemixSpringBootJPA" target="_blank"><img src="http://bluemix.net/deploy/button.png" alt="Bluemix button" /></a>

<h2> Etapas para executar localmente </h2>

- Código de Clone, como se segue

```
> git clone https://github.com/thimico/BluemixSpringBootJPA.git
```

- Editar o arquivo  src/main/resources/spring-cloud-bootstrap.properties

Aqui você precisa especificar o caminho para o seu  arquivo "spring-cloud-mysql.properties", você vai precisar para criar esse arquivo
com conteúdo da seguinte forma. A localização pode ser em qualquer lugar em seu sistema de arquivos e qualquer nome de arquivo.

```
spring.cloud.propertiesFile: /Users/thimico/Documents/spring-cloud-mysql.properties
```

3.2. Editar o arquivo para garantir que você adicione seus detalhes MySQL local, se o seu usando as configurações padrão do MySQL em seu laptop ou desktop abaixo é tudo que você precisa

```
spring.cloud.appId: SpringBootMYSQLLocal
spring.cloud.database: mysql://root:root@localhost:3306/teste
spring.datasource.max-active: 10
spring.datasource.initial-size: 1
```
 
- Rode o comando

```
> mvn package
```

- Execute o seguinte comando

```
mvn spring-boot:run
```

- Acesso a seguinte url

```
http://localhost:8080/
```

<h2> Implantar no IBM Bluemix  </h2>

- Ao implantar a IBM Bluemix você deve ligar o aplicativo para um serviço MYSQL como mostrado na manifest.yml abaixo.

```
applications:
- name: demo-albums
  memory: 512M
  instances: 1
  host: demo-albums
  path: ./target/BluemixSpringBootJPA-0.0.1-SNAPSHOT.jar
  services:
    - seu-mysql
```

Nota: O arquivo de manifesto a seguir pressupõe que você tenha um serviço MYSQL chamado "seu-mysql", então você vai precisar de um serviço de MYSQL
criado e certifique-se de usar o nome do serviço corretamente


```
Pronto
