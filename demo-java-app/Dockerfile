# --- Étape de build ---
FROM maven:3.9.5-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn -q -e -DskipTests clean package

# --- Étape de runtime ---
FROM eclipse-temurin:17-jdk
WORKDIR /app
COPY --from=build /app/target/demo-java-app.jar app.jar
# On utilise 8081 pour éviter le conflit avec Jenkins (8080)
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
