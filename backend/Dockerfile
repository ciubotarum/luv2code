# Use a base image with Java and Maven installed
FROM maven:3.9.6-eclipse-temurin-21 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the pom.xml and download the dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Use a lightweight base image with Java installed
FROM maven:3.9.6-eclipse-temurin-21

# Set the working directory in the container
WORKDIR /app

# Copy the built JAR file from the previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose the port that the application listens on
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]

# docker build -t my-backend-app .

# docker my-backend-app