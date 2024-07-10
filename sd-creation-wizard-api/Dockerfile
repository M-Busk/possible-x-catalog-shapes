#  Copyright 2023-2024 Dataport AöR
#
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

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
