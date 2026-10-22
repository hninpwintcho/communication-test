# Stage 1: Build the Spring Boot application
FROM maven:3.9.6-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml ./
RUN mvn dependency:go-offline

COPY src ./src/
RUN mvn clean package -DskipTests


# Stage 2: Runtime
FROM eclipse-temurin:21-jre

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
EXPOSE 14000-14050/udp
EXPOSE 15000-15050/udp

CMD ["java", "-jar", "app.jar"]
