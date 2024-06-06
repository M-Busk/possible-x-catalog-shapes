FROM maven:3-eclipse-temurin-17-alpine AS build

RUN apk add --no-cache git maven &&\
    git clone https://gitlab.eclipse.org/eclipse/xfsc/self-description-tooling/sd-creation-wizard-api.git &&\
    cd /sd-creation-wizard-api &&\
    git checkout 8b57ef8a88d0bc71513fd3ca15760755189fa316 &&\
    mvn clean package -Dmaven.test.skip=true

FROM eclipse-temurin:17-jre-alpine
COPY --from=build /sd-creation-wizard-api/target/creation-wizard-api*.jar /opt/creation-wizard-api.jar
COPY catalog-shapes/shacl/shapes/gx/ /shapes/gx/
COPY catalog-shapes/shacl/shapes/merlot/ /shapes/merlot/

ENTRYPOINT ["java", "-jar","/opt/creation-wizard-api.jar"]
