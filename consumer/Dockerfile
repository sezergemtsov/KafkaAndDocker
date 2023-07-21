FROM amazoncorretto:17-alpine3.15-jdk

#Port
EXPOSE 8080

#Application
ADD kafkaCon-0.0.1-SNAPSHOT.jar consumer.jar

#Start
ENTRYPOINT ["sh", "-c", "sleep 30; java -jar /consumer.jar"]
