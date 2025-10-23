# Étape 1 : Build du projet
FROM maven:3.9.9-eclipse-temurin-21 AS builder
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline -B

COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Image d'exécution
FROM eclipse-temurin:21-jdk AS runner
WORKDIR /app

# Copier le jar compilé depuis l’étape builder
COPY --from=builder /app/target/api-gateway-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 4004
ENTRYPOINT ["java", "-jar", "app.jar"]
