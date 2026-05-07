FROM maven:3.9.9-eclipse-temurin-21 AS analyticsBuilder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package

FROM eclipse-temurin:21-jdk  AS analyticsRunner

WORKDIR /app

COPY --from=analyticsBuilder ./app/target/analytics-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4002

ENTRYPOINT ["java", "-jar", "app.jar"]
