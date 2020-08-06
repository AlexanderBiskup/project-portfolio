# IoT Analysis Cloud

# 1. Introduction

The IoT Analysis Cloud is a collection of microservices with the purpose of collecting, analyzing, monitoring and visualizing data produced by IoT devices. This project is the result of an university assignment and was designed and implemented by a group of four students, including me. 

The main goals of this assignment were to: 

1. Implement a distributed software system using established patterns and techniques
2. Use a microservice architecture to implement the required functionality
3. Design and implement a message queue and a respective asynchronous protocol to introduce a layer of indirection for the communication between the microservices

# 2. Microservices

For this assignment it was required to implement five microservices. Full details about the microservices can be found in the [assignment sheet](https://github.com/AlexanderBiskup/iot-analysis-cloud/blob/master/assignment_sheet.pdf).

## 2.1. MS1 - Message Queue

The Message Queue allows other microservices to subscribe and publish messages. The following features are supported:

- Publish/Subscribe
- Delayed Delivery
- Asynchronous push based communication
- Delayed Receive
- Message Prioritization
- Termination Messages

## 2.2. MS2 - Message Queue Monitoring Component

This microservices connects to MS1 and observes events about client connections, messages and errors. Monitoring sessions can also publish termination messages to shutdown connected clients of the message queue.

To interact with MS2 we implemented a cli-application called **ms2-cli-client**. 

## 2.3. MS3 - Result Output Service

The Result Output Services subscribes to messages of the Machine Learning Service (MS4), which contain the analyzed data and makes them available to a web client called **ms3-web-client** for visualization. 

## 2.4. MS4 - Machine Learning Service

This microservice subscribes to messages of the IoT Simulation Service (MS5) and performs predictions and anomaly detection on the data produced by MS5. It then publishes predictions and anomaly warnings (consumed by MS3). 

## 2.5. MS5 - IoT Simulation Service

This service simulates basic IoT-sensors which produce and publish, depending on the configuration, either temperature or light intensity data. 

# 3. Project Repository

https://github.com/AlexanderBiskup/iot-analysis-cloud

# 4. Tech Stack

**Microservices**: Kotlin JVM + Spring Boot (Spring Web, Spring WebSocket)

**ms2-cli-client**: Kotlin JVM + Spring Shell

**ms3-web-client**: html + javascript

# 5. Demo

## 5.1. Requirements

To be able to run the demo the following requirements have to be installed on your machine:

1. [Docker](https://docs.docker.com/desktop/) (v19.03.8)
2. [Docker Compose](https://docs.docker.com/compose/install/) (version 1.25.4)

## 5.2. How to start up the applications

Please make sure the Docker Engine is up and running

1. Clone the repository 
```bash
git clone https://github.com/AlexanderBiskup/iot-analysis-cloud
```

2. Go to the project directory
```bash
cd iot-analysis-cloud
```

3. Checkout the demo branch
```bash
git checkout -b demo remotes/origin/demo
```

4. Go to the demo directory
```bash
cd demo
```

5. Build the project by running the build script (this may take a few minutes)
```bash
./build.sh
```

6. Start MS1
```bash
docker-compose up ms1
```

7. Start MS2 in a new terminal window
```bash
docker-compose up ms2
```

8. Start ms2-cli-client in new terminal window
```bash
docker-compose run --rm ms2-cli-client
```

9. Start MS3, ms3-web-client, MS4 and MS5 in a new terminal window
```bash
docker-compose up ms3 ms3-web-client ms4 ms5
```

## 5.3. Guided Demo

Please make sure you followed the [start up instructions](#52-how-to-start-up-the-applications).

1. Visit the ms3-web-client at http://localhost:8080 and click "Connect". You should now see the temperature data graph. You can toggle to temperature analyzed in the top-left corner to see the predictions produced by MS4.
2. Go to the terminal window where you started ms2-cli-client. 
3. Use the command "messages" to see how many messages have been exchanged so far.
4. Use the command "clients" to see details about the connected clients.
5. Copy the id of one client and use the command "terminate-client --id \<client-id\>]". The service you've selected should shutdown immediately and the message flow should stop.