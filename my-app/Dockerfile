FROM maven:3.6.3-openjdk-8-slim AS build
ARG JAR_VERSION
RUN mkdir -p /workspace
WORKDIR /workspace
COPY pom.xml /workspace
COPY src /workspace/src
RUN mkdir target
RUN mvn -B package -DskipTests -Dversion=1.0.${JAR_VERSION} -Dpackaging=jar -DoutputDirectory=target --file pom.xml

FROM openjdk:8-slim
ARG JAR_VERSION 
COPY --from=build /workspace/target/my-app-1.0.${JAR_VERSION}.jar my-app.jar
RUN chmod 777 my-app.jar
RUN useradd -u 1000 elhay
# Change to non-root privilege
USER elhay
ENTRYPOINT ["java","-jar","my-app.jar"]
