FROM maven:3.6.3-openjdk-8-slim AS build
RUN mkdir -p /workspace
WORKDIR /workspace
COPY app/pom.xml /workspace
COPY app/src /workspace/src
RUN mvn -B package --file pom.xml -DskipTests

FROM openjdk:8-slim
COPY --from=build /workspace/target/*jar-with-dependencies.jar app.jar
EXPOSE 6379
ENTRYPOINT ["java","-jar","app.jar"]