## KafkaAndDocker  
### Short description
This project used standard kafka serverv with kraft and without SSL to send and recieve messages  
For kafka server was used image amazoncorretto:11-alpine-jdk  
The same image used as base for simple Spring applications: producer and consumer. Producer has controller with default endpoint: "localhost:8080/message" that carry key "text" and String message as qeiry params. Also controller set with POST request so it doesnt work from browser.  
Consumer app reflect list of messages on default port localhost:8081. It is blocking app so page suppose to update.
### Start application
3 services works as divided containers, and are using docker-compose.yaml so to start app, on host must be docker and additionaly docker compose in case of linux.
Download repository, open that folder and open console. Than send console command "docker compose up" and wait about 1 min while all containers start.  
Now you can use endpoints to check app!
