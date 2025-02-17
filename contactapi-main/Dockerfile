# Use a valid Maven image
FROM maven:3.8.8-openjdk-21-slim AS builder

# Set working directory inside the container
WORKDIR /app

# Copy the pom.xml and source code
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Create a minimal runtime image
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY --from=builder /app/target/contactapp.jar /app/contactapp.jar
CMD ["java", "-jar", "/app/contactapp.jar"]
