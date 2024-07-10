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

ARG SERVICE_VERSION=a37ab257ebda35c80ccf27d65294aef8df53e4e5

COPY catalog-shapes/ /catalog-shapes/

RUN apk add --no-cache python3 py3-rdflib &&\
    cd /catalog-shapes &&\
    python3 merge_shapes.py

COPY gxfs-catalog/truncate_schemas.patch /truncate_schemas.patch
COPY gxfs-catalog/optional_registry.patch /optional_registry.patch
COPY gxfs-catalog/ignore-compliance-signature.patch /ignore-compliance-signature.patch
COPY gxfs-catalog/ignore-compliance-claims.patch /ignore-compliance-claims.patch

RUN apk add --no-cache git maven &&\
    git clone -b main https://gitlab.eclipse.org/eclipse/xfsc/cat/fc-service.git &&\
    cd /fc-service &&\
	git checkout $SERVICE_VERSION &&\
	git apply /truncate_schemas.patch &&\
    git apply /optional_registry.patch &&\
    git apply /ignore-compliance-signature.patch &&\
    git apply /ignore-compliance-claims.patch &&\
    rm -rf fc-service-core/src/main/resources/defaultschema/ontology &&\
    rm fc-service-core/src/main/resources/defaultschema/shacl/mergedShapesGraph.ttl &&\
    cp /catalog-shapes/shacl/shapes/mergedShapes.ttl fc-service-core/src/main/resources/defaultschema/shacl/mergedShapesGraph.ttl &&\
    cp -r /catalog-shapes/shacl/ontology fc-service-core/src/main/resources/defaultschema/ontology &&\
    mvn clean package -pl fc-service-server -am -Dmaven.test.skip=true

FROM eclipse-temurin:17-jre-alpine
COPY --from=build /fc-service/fc-service-server/target/fc-service-server-*.jar /opt/fc-service-server.jar
ENTRYPOINT ["java", "-jar","/opt/fc-service-server.jar"]
