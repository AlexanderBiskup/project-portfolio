# MeetIn

# 1. Introduction
MeetIn is a web application for managing and coordinating appointments related to projects. 
It allows users to create projects, invite project members and let them vote for potential appointments.
This is a personal project of myself which I used for experimenting with React and React hooks.

# 2. Project repository
https://gitlab.com/AlexBiskup/meet-in

# 3. Tech Stack
## 3.1. Frontend
- Typescript 
- React (with hooks)
- Semantic UI

## 3.2. REST API
- Kotlin JVM
- Spring Boot (Web, Security, Data JPA, Flyway)
- MySQL

# 4. Demo
## 4.1. Requirements

To be able to run the demo the following requirements have to be installed on your machine:

1. [Docker](https://docs.docker.com/desktop/) (v19.03.8)
2. [Docker Compose](https://docs.docker.com/compose/install/) (version 1.25.4)

## 4.2. How to start up the applications

Please make sure the Docker Engine is up and running

1. Clone the repository 
```bash
git clone https://gitlab.com/AlexBiskup/meet-in
```

2. Go to the project directory
```bash
cd meet-in
```

3. Checkout the demo branch
```bash
git checkout -b demo remotes/origin/demo
```

4. Go to the demo directory
```bash
cd demo
```
5. Build frontend and REST API by running the build script (this may take a few minutes)
```bash
./build.sh
```

6. Start the apps with docker
```bash
docker-compose up
```

## 4.3. Guided Demo
In this demo you are going to log in to existing accounts, create and vote for appointments.

Please make sure you followed the [start up instructions](#42-how-to-start-up-the-applications).


1. Visit the React frontend at http://localhost:3000
2. Log in with Email **john.deacon@gmail.com** and Passwort **johndeacon**
3. Find and click the project "Queen Konzerttermine" beneath "Teilnahmen" - you should be able to see the appointments for this project and their status.
   If you click on an appointment you can see how each member voted for that particular appointment. 
4. Select "Abstimmen" above the appointments and vote for the remaining appointment by dragging and dropping it.
5. Go back to projects and log out
6. Log in with Email **freddie.mercury@gmail.com** and Passwort **freddie**
7. Select the project "Queen Konzerttermine" beneath "Meine Projekte" - 
   Freddie is the owner of this project, so he can also change the overall status of an appointment (not only his vote) by dragging and dropping.
   Once you change the status of an appointment to anything other then "Offen", the members won't be able to vote for it anymore.
   The owner can also right click on an appointment and edit it.
8. Create a new appointment by clicking "Neuer Termin"

You can also explore the settings of the project by selecting "Einstellungen"
