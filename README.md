# FIAP Checkpoint 2

Projeto desenvolvido para o Checkpoint 2 da FIAP utilizando Java e Spring Boot.

A aplicação foi estruturada utilizando uma arquitetura baseada em Spring Boot, com persistência de dados através do Spring Data JPA e suporte a diferentes ambientes de execução.

## 🚀 Tecnologias

* Java 17
* Spring Boot 3.2.4
* Spring Web
* Spring Data JPA
* Thymeleaf
* Hibernate
* H2 Database
* MySQL
* Maven
* Docker

## 📋 Sobre o projeto

O projeto consiste em uma aplicação desenvolvida com Spring Boot para gerenciamento de informações relacionadas a pacientes, profissionais e consultas.

O domínio principal da aplicação é composto pelas entidades:

* Paciente
* Profissional
* Consulta

Uma consulta possui relacionamento com um paciente e um profissional, além de informações como data, status, quantidade de horas e valor da consulta.

A entidade `Consulta` possui relacionamentos `ManyToOne` com `Paciente` e `Profissional`, enquanto os dados são mapeados utilizando Jakarta Persistence (JPA).

## 🏗️ Estrutura do projeto

```text
fiap-checkpoint2/
├── .mvn/
│   └── wrapper/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── br/com/fiap/checkpoint2/
│   │   │       ├── controller/
│   │   │       │   └── CheckpointController.java
│   │   │       │
│   │   │       ├── model/
│   │   │       │   ├── AbstractEntity.java
│   │   │       │   ├── Consulta.java
│   │   │       │   ├── Paciente.java
│   │   │       │   └── Profissional.java
│   │   │       │
│   │   │       ├── util/
│   │   │       │   └── StatusConsulta.java
│   │   │       │
│   │   │       └── Checkpoint2Application.java
│   │   │
│   │   └── resources/
│   │       ├── application-dev.properties
│   │       ├── application-stg.properties
│   │       └── application-prd.properties
│   │
│   └── test/
│       └── java/
│
├── Dockerfile
├── .gitignore
├── mvnw
├── mvnw.cmd
├── pom.xml
└── README.md
```

A organização atual do código separa controllers, models e utilitários, além de manter arquivos de configuração específicos para cada ambiente.

## 📦 Modelo de dados

### Paciente

A entidade `Paciente` representa os pacientes cadastrados na aplicação.

Principais informações:

* Nome
* Endereço
* Bairro
* E-mail
* Telefone
* Data de nascimento
* Data de criação
* Data de atualização

A entidade é persistida na tabela `pacientes`.

### Profissional

A entidade `Profissional` representa os profissionais responsáveis pelos atendimentos.

Principais informações:

* Nome
* Especialidade
* Valor por hora
* Data de criação
* Data de atualização

A entidade é persistida na tabela `profissionais`.

### Consulta

A entidade `Consulta` representa o atendimento realizado entre um paciente e um profissional.

Principais informações:

* Profissional responsável
* Paciente
* Data da consulta
* Status da consulta
* Quantidade de horas
* Valor da consulta

A entidade é persistida na tabela `consultas`.

## 🔗 Relacionamentos

O relacionamento principal do modelo pode ser representado da seguinte forma:

```text
Paciente
   │
   │ 1
   │
   │ N
Consulta
   │
   │ N
   │
   │ 1
Profissional
```

Uma consulta pertence a um paciente e a um profissional.

## ⚙️ Configuração dos ambientes

A aplicação possui três arquivos de configuração:

```text
application-dev.properties
application-stg.properties
application-prd.properties
```

O ambiente é definido através da variável `PROFILE`.

### Desenvolvimento

O ambiente `dev` utiliza um banco H2 em memória:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
```

Também possui o console do H2 habilitado e configuração para criação automática das tabelas.

### Staging

O ambiente `stg` está configurado para utilizar MySQL:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/rh
```

As configurações de JPA utilizam `ddl-auto=update`, permitindo a atualização do schema conforme as entidades.

### Produção

O ambiente `prd` possui um arquivo de configuração próprio, permitindo separar as configurações utilizadas em produção das configurações de desenvolvimento e staging.

## 💻 Executando localmente

### Pré-requisitos

Para executar o projeto localmente, é necessário ter instalado:

* Java 17
* Maven ou Maven Wrapper
* Git

### Clonando o projeto

```bash
git clone https://github.com/gustavoconce/fiap-checkpoint2.git
```

Entre na pasta do projeto:

```bash
cd fiap-checkpoint2
```

### Executando com Maven

No Windows:

```bash
mvnw.cmd spring-boot:run
```

No Linux/macOS:

```bash
./mvnw spring-boot:run
```

## 🐳 Docker

O projeto possui um `Dockerfile` para criação da imagem e execução da aplicação em container. O container expõe a porta `8080`.

### Construindo a imagem

```bash
docker build -t cssgustavo/fiap-checkpoint2 .
```

### Execução em DES

```bash
docker run -d -p 8080:8080 -e PROFILE=dev cssgustavo/fiap-checkpoint2
```

### Execução em STG

```bash
docker run -d -p 8080:8080 -e PROFILE=stg cssgustavo/fiap-checkpoint2
```

### Execução em PRD

```bash
docker run -d -p 8080:8080 -e PROFILE=prd cssgustavo/fiap-checkpoint2
```

## 🔧 Maven

O projeto utiliza Maven para gerenciamento de dependências e build da aplicação.

Entre as principais dependências estão:

* `spring-boot-starter-web`
* `spring-boot-starter-data-jpa`
* `spring-boot-starter-thymeleaf`
* `spring-boot-starter-test`
* H2 Database
* MySQL Connector
* Spring Boot DevTools

A versão do Java configurada no projeto é a 17 e o projeto utiliza Spring Boot 3.2.4.

## 🧪 Testes

Os testes automatizados ficam organizados em:

```text
src/test/java/br/com/fiap/checkpoint2
```

Para executar os testes:

```bash
./mvnw test
```

No Windows:

```bash
mvnw.cmd test
```

## ▶️ Porta da aplicação

Por padrão, a aplicação utiliza a porta:

```text
8080
```

Após iniciar a aplicação, ela pode ser acessada em:

```text
http://localhost:8080
```

## 📚 Objetivos acadêmicos

Este projeto foi desenvolvido como parte das atividades acadêmicas da FIAP, colocando em prática conceitos relacionados a:

* Desenvolvimento de aplicações Java
* Spring Boot
* Spring Data JPA
* Mapeamento objeto-relacional
* Desenvolvimento Web
* Persistência de dados
* Banco de dados
* Configuração de ambientes
* Containerização com Docker

## 👨‍💻 Autor

**Gustavo Santos Conceição**

Graduado em Sistemas de Informação pela FIAP.

GitHub: [@gustavoconce](https://github.com/gustavoconce)

---

## 📌 Status do projeto

🚧 Em desenvolvimento.

O projeto poderá receber novas funcionalidades e melhorias conforme a evolução das atividades e dos estudos relacionados ao desenvolvimento backend com Java e Spring Boot.
