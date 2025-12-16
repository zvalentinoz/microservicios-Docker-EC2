FROM eclipse-temurin:17-jdk-alpine AS builder

WORKDIR /app

COPY pom.xml .

COPY msvc-usuarios/.mvn msvc-usuarios/.mvn
COPY msvc-usuarios/mvnw msvc-usuarios/mvnw
COPY msvc-usuarios/pom.xml msvc-usuarios/pom.xml

RUN chmod +x msvc-usuarios/mvnw

RUN cd msvc-usuarios && ./mvnw dependency:go-offline

COPY msvc-usuarios/src msvc-usuarios/src

RUN cd msvc-usuarios && ./mvnw clean package -DskipTests


FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=builder /app/msvc-usuarios/target/msvc-usuarios-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8001
ENTRYPOINT ["java","-jar","app.jar"]
