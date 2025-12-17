# 1: Maven을 사용해 java 프로젝트 빌드
FROM maven:3.8.5-openjdk-8-slim AS build
WORKDIR /app
COPY src ./src
COPY pom.xml .
RUN mvn -f pom.xml clean package

# 2: 빌드된 jar 파일을 가져와 컨테이너 이미지 생성
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE=/app/target/*.jar
COPY --from=build ${JAR_FILE} app.jar
EXPOSE 8090
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]