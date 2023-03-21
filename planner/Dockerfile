#################################################
# Imagen base para el contenedor de compilación
#################################################
FROM maven:3.9.0-eclipse-temurin-17 as builder

# Define el directorio de trabajo donde ejecutar comandos
WORKDIR /project

# Copia las dependencias del proyecto
COPY pom.xml /project/

# Copia el código del proyecto
COPY /src /project/src

# Compila proyecto y descarga librerías
RUN mvn -B package -DskipTests

#################################################
# Imagen base para el contenedor de la aplicación
#################################################
FROM eclipse-temurin:17-jdk

# Define el directorio de trabajo donde se encuentra el JAR
WORKDIR /usr/src/app/

# Copia el JAR del contenedor de compilación
COPY --from=builder /project/target/planner-0.0.1-SNAPSHOT.jar /usr/src/app/

# Indica el puerto que expone el contenedor
EXPOSE 8080

# Comando por defecto
ENTRYPOINT [ "java", "-jar", "planner-0.0.1-SNAPSHOT.jar" ]

# Parametro por defecto
CMD ["--server"]