FROM alpine/java:21-jdk AS build
WORKDIR /backend

COPY gradlew gradlew
COPY gradle gradle
COPY build.gradle.kts build.gradle.kts
COPY settings.gradle.kts settings.gradle.kts

RUN ./gradlew --no-daemon dependencies || true

COPY src src

RUN ./gradlew --no-daemon bootJar -x test

FROM alpine/java:21-jdk AS runtime
WORKDIR /backend

COPY --from=build /backend/build/libs/*.jar backend.jar

EXPOSE 8000

ENTRYPOINT [ "java", "-jar", "backend.jar"]
