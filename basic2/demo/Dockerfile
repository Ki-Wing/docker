#멀티 스테이지 빌드 방법 사용
#첫번째 스테이지
FROM openjdk:11 AS stage1

WORKDIR /app

#/app/gradlew로  생성
COPY gradlew .
#/app/gralde 폴더로 생성
COPY gradle gradle
COPY src src
COPY build.gradle .
COPY settings.gradle .

#도커컨테이너 내에서 명령어 사용
RUN ./gradlew bootJar



#두번째 스테이지
FROM openjdk:11
WORKDIR /app
#jar파일이 들어가는 루트.. stage1에 있는 jar을 stage2의 app.jar라는 이름으로 copy
COPY --from=stage1 /app/build/libs/*.jar app.jar

#CMD 또는 ENTRYPORINT(복잡한게 더 많음)를 통해 컨테이너를 실행
ENTRYPOINT ["java", "-jar", "app.jar"]

#docker컨테이너 내에서 밖의 전체 host를 저장하는 도메인 : host.docker.internal
#    yml파일 바꾸는대신 실행하는 시점에서 변경 // yml 위치 말함.
#docker run -d -p 8081:8080 -e SPRING_DATASOURCE_URL=jdbc:mariadb://host.docker.internal:3306/board spring_test:latest

#docker컨테이너 실행 시에 볼륨을 설정할 때에는 -v 옵션 사용
#docker run -d -p 8081:8080 -e SPRING_DATASOURCE_URL=jdbc:mariadb://host.docker.internal:3306/board -v C:\Users\Playdata\Desktop\tmp_logs:/app/logs spring_test:latest





