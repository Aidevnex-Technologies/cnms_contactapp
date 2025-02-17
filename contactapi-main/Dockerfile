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

# Add a debug step to list the files and confirm if the JAR is created
RUN ls -al /app/target/

# Step 6: Create the runtime image
FROM openjdk:21-jdk-slim
WORKDIR /app

# Debugging: List the files inside the target directory to check JAR existence
COPY --from=builder /app/target/ /app/target/
RUN ls -al /app/target/

# Step 7: Copy the JAR from the build stage
COPY --from=builder /app/target/contactapp.jar /app/contactapp.jar

# Step 8: Command to run the application
CMD ["java", "-jar", "/app/contactapp.jar"]
