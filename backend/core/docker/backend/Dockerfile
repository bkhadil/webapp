FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline -B

COPY src ./src
RUN mvn clean package -DskipTests -DMAVEN_OPTS="-Xmx1024m"

FROM eclipse-temurin:21-jre-alpine
RUN apk add --no-cache bash



COPY --from=build /app/target/*.jar /app/app.jar

CMD ["java", "-jar", "/app/app.jar"]

