FROM eclipse-temurin:17-jdk-alpine AS builder

WORKDIR /app

# Copiamos POM padre (solo para resolver parent)
COPY pom.xml .

# Copiamos Maven Wrapper DEL MÓDULO
COPY msvc-cursos/.mvn msvc-cursos/.mvn
COPY msvc-cursos/mvnw msvc-cursos/mvnw
COPY msvc-cursos/pom.xml msvc-cursos/pom.xml

RUN chmod +x msvc-cursos/mvnw

# Descarga dependencias
RUN cd msvc-cursos && ./mvnw dependency:go-offline

# Código fuente
COPY msvc-cursos/src msvc-cursos/src

# Build del módulo
RUN cd msvc-cursos && ./mvnw clean package -DskipTests


FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=builder /app/msvc-cursos/target/msvc-cursos-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8002
ENTRYPOINT ["java","-jar","app.jar"]
