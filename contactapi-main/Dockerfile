# Step 1: Use OpenJDK 21 as the base image
FROM openjdk:21-jdk-slim AS builder

# Step 2: Install Maven
RUN apt-get update && apt-get install -y maven

# Step 3: Set the working directory inside the container
WORKDIR /app

# Step 4: Copy the pom.xml and the source code into the container
COPY pom.xml .
COPY src ./src

# Step 5: Build the application using Maven
RUN mvn clean package -DskipTests

# Step 6: Create the runtime image
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY --from=builder /app/target/contactapp.jar /app/contactapp.jar

# Step 7: Command to run the application
CMD ["java", "-jar", "/app/contactapp.jar"]
