FROM java:8

EXPOSE 8080

ADD target/department-service.jar department-service.jar

ENTRYPOINT ["java","-jar","department-service.jar"]