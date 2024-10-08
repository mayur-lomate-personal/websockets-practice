# Load Balanced WebSocket with Authorization and Rabbitmq message broker to send messages to a particular user

• This project demonstrates how to implement WebSocket load balancing with authentication, using a message broker to efficiently handle and distribute messages for reliable real-time communication,resembling messaging applications.

• Implemented user authentication using JWT (JSON Web Tokens), enhancing security by ensuring that only authenticated users are allowed to connect to WebSocket endpoints.

• RabbitMQ is used as the message broker due to its robust support for scalable and reliable message queuing, and the protocol employed for communication is STOMP

• In this project, I implemented the capability to send targeted messages to individual users, as well as the option to broadcast messages to all users simultaneously, providing flexible communication options tailored to specific needs.

## Run

- Docker
```docker
docker compose up -id
```
- minikube
```minikube
(open terminal and be at path of minikube folder)
kubectl apply -f .\bootstrap\postgres\
kubectl apply -f .\bootstrap\rabbitmq\
minikube service --url rabbitmq
(create admin user in rabbitmq and give all permissions)
kubectl apply -f .\services\database\
kubectl apply -f .\services\authoriser\
kubectl apply -f .\services\websocket\
minikube service --url authoriser-server
minikube service --url websocket-server
```

## APIs

```http
POST [gateway-url]:[gateway-port]/api/register/user :- To create new user
```
```http
POST [gateway-url]:[gateway-port]/api/jwt :- To get jwt token
```
```http
GET [gateway-url]:[gateway-port]/api/websocket/session :- to get session token valid for 30 seconds, used for websocket.
```
## System Design
![websocket-system-design](https://user-images.githubusercontent.com/77961230/197375506-368fdc6a-5d72-4141-aa7a-e832c400ae36.jpg)

## System Design(Kubernetes)
![kubernetes-websocket-system-design](./k8s/messanger-based-on-websocket-kubernetes.drawio.png)