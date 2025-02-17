# Use Maven to build the application
FROM maven:3.8.8-openjdk-21 AS builder

# Set working directory inside the container
WORKDIR /app

# Copy the Maven project files
COPY contactapi-main/pom.xml .

# Download dependencies (this helps with build caching)
RUN mvn dependency:go-offline -B

# Copy the rest of the project files
COPY contactapi-main/ .

# Build the application (without running tests)
RUN mvn clean package -DskipTests

# Use a lightweight JDK runtime for the final image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the builder stage
COPY --from=builder /app/target/contactapi-main.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]
