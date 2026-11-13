# Etapa 1: compilacao do projeto com Java 21
FROM eclipse-temurin:21-jdk AS build

WORKDIR /app

COPY .mvn/ .mvn/
COPY mvnw pom.xml ./

# Corrige quebras de linha do Windows no Maven Wrapper
RUN sed -i 's/\r$//' mvnw && chmod +x mvnw

COPY src/ src/

# Compila o projeto e executa os testes
RUN ./mvnw -B -ntp clean package


# Etapa 2: execucao da aplicacao
FROM eclipse-temurin:21-jre

WORKDIR /app

# Copia o JAR gerado na etapa anterior
COPY --from=build /app/target/backend-0.0.1-SNAPSHOT.jar /app/app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/app.jar"]