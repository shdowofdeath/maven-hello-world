FROM maven:3.6.3-openjdk-8-slim AS build
ARG version
RUN mkdir -p /workspace
WORKDIR /workspace
COPY app/pom.xml /workspace
COPY app/src /workspace/src
RUN mvn -B package --file pom.xml -DskipTests
RUN mvn -B package -DskipTests -Dversion=1.0.${{ github.run_number }} -Dpackaging=jar -DoutputDirectory=target --file pom.xml

FROM openjdk:8-slim
ARG version
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 6379
ENTRYPOINT ["java","-jar","app.jar"]