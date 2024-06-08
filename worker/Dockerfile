FROM maven:3.9.6-eclipse-temurin-21-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:resolve
COPY src src
RUN mvn package && \
    mv target/worker-jar-with-dependencies.jar /app/worker.jar

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/worker.jar .
CMD ["java", "-jar", "worker-jar-with-dependencies.jar"]
