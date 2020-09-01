# Money In Money Out

# 1. Introduction

Money In Money Out is a web application which tracks accounts and expenses. 
This project is the result of an university assignment and was designed and implemented by a group of four students, including me. 

The main goals of this assignment were to: 

1. Create a web application which offers basic CRUD operations using a relational database
2. Create a second version of the same application using a NoSQL database
3. Generate a considerable amount of datasets for every table automatically
4. Implement a application-level migration mechanism to migrate the data stored in the relational database to the NoSQL database

# 2. Project Repository

https://gitlab.com/AlexBiskup-university/mimo.git

### 2.1. Branches

- **master**: contains the relational database version
- **mongodb-version**: contains the NoSQL database version
- **demo**: contains configuration files for starting the demo

# 3. Tech Stack

## 3.1. Relational Database Version

- Web application: Java 8 + Spring Boot (Spring Web, Spring JPA, Thymeleaf, Spring Security, Flyway)
- Database: MySQL 5.7
- Build tool: Gradle

## 3.2. NoSQL Database Version

- Web appliation: Java 8 + Spring Boot (Spring Web, Spring Data MongoDB, Thymeleaf, Spring Security)
- Database: MongoDB
- Build tool: Gradle

# 4. Demo

## 4.1. Requirements

To be able to run the demo the following requirements have to be installed on your machine:

1. [Docker](https://docs.docker.com/desktop/) (v19.03.8)
2. [Docker Compose](https://docs.docker.com/compose/install/) (version 1.25.4)

## 4.2. How to start up the applications

Please make sure the Docker Engine is up and running

1. Clone the repository 

```bash
git clone https://gitlab.com/AlexBiskup-university/mimo.git
```

2. Go to the project directory

```bash
cd mimo
```

3. Checkout the demo branch

```bash
git checkout demo
```

4. Go to the demo directory

```bash
cd demo
```

5. Start docker containers

```bash
docker-compose up
```

## 4.3. Guided Demo

In this demo you're going to generate multiple datasets automatically, create a user, an account and a payment manually, and migrate the data to the NoSQL application.

Please make sure you followed the [start up instructions](#42-how-to-start-up-the-applications).

### 4.3.1. Prepare Data

1. Visit [mimo-mysql](http://localhost:8080)
2. Login as admin user: Username: **admin**, Password: **admin**
3. Go to the [data generator](http://localhost:8080/generator) at path "/generator".
4. Fill the form (10 users, 2 acccounts per user, 50 payments per accounts, 20 categories) and click Generate
5. Go to [Users](http://localhost:8080/users)
6. Click Add User, fill the form and submit
7. Logout and login again with the newly created user
8. Click New Account and fill and submit the form
9. Find your account in the list and click Payments
10. Click Add Payment, fill the form and click submit

### 4.3.2. Migrate Data

1. Visit [mimo-mongodb](http://localhost:8090)
2. Login as admin user: Username: **admin**, Password: **admin**
3. Verify that no data is currently present
4. Go to the [migration tool](http://localhost:8090/migration) at path "/migration" and click Migrate
5. Logout and login again with the user you created in mimo-mysql
6. Verify your data is there