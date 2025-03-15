FROM gradle:7-jdk17 AS base

CMD ["bash"]

# build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
# buildだけでなく、テストも実行する
RUN ./gradlew build

# production
FROM openjdk:17 AS production
COPY --from=test-and-build /workspace/build/libs/api-0.0.1-SNAPSHOT.jar ./api.jar
CMD [ "java", "-jar", "api.jar" ]