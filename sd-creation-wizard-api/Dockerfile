#  Copyright 2024 Dataport. All rights reserved. Developed as part of the MERLOT project.
#  Copyright 2024-2025 Dataport. All rights reserved. Extended as part of the POSSIBLE project.
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

COPY sd-creation-wizard-api/add_regex_support.patch /add_regex_support.patch

RUN apk add --no-cache git maven &&\
    git clone https://gitlab.eclipse.org/eclipse/xfsc/self-description-tooling/sd-creation-wizard-api.git &&\
    cd /sd-creation-wizard-api &&\
    git checkout bf7a35f8b763d3a198a8d586da93b27d61f3fc2a &&\
    git apply /add_regex_support.patch &&\
    mvn clean package -Dmaven.test.skip=true

FROM eclipse-temurin:17-jre-alpine
COPY --from=build /sd-creation-wizard-api/target/creation-wizard-api*.jar /opt/creation-wizard-api.jar
COPY catalog-shapes/shacl/shapes/ /shapes/

ENTRYPOINT ["java", "-jar","/opt/creation-wizard-api.jar"]
