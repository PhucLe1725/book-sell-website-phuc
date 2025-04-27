# Build stage
FROM maven:3-openjdk-21 AS build
WORKDIR /app

# Copy pom.xml và download dependencies để cache
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy source code
COPY src ./src

# Build ứng dụng (skip test để nhanh hơn)
RUN mvn clean package -DskipTests

# Run stage
FROM openjdk:21-jdk-slim
WORKDIR /app

# Copy file jar từ build stage
COPY --from=build /app/target/test-0.0.1-SNAPSHOT.jar app.jar

# Expose đúng cổng 8090
EXPOSE 8090

# Chạy app
ENTRYPOINT ["java", "-jar", "app.jar"]
