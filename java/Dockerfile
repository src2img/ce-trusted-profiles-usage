FROM ibm-semeru-runtimes:open-21-jdk AS builder

# Install Maven
ARG MAVEN_VERSION=3.9.9
RUN \
  mkdir /tmp/maven && \
  curl -fsSL "https://dlcdn.apache.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz" | tar -xzf - -C /tmp/maven --strip-components=1

COPY . /src
WORKDIR /src
RUN /tmp/maven/bin/mvn package -Dmaven.test.skip=true

# Overwrite ContainerAuthenticator
RUN apt update && apt install -y zip
ADD https://github.com/SaschaSchwarze0/ibm-java-sdk-core.git#sascha-containerauthenticator-codeengine /ibm-java-sdk-core
WORKDIR /ibm-java-sdk-core
RUN \
  /tmp/maven/bin/mvn compile && \
  cd target/classes && \
  zip /src/target/trustedprofiles-1.0-SNAPSHOT.jar com/ibm/cloud/sdk/core/security/ContainerAuthenticator*

FROM ibm-semeru-runtimes:open-21-jre

COPY --from=builder /src/target/trustedprofiles-1.0-SNAPSHOT.jar /app/trustedprofiles-1.0-SNAPSHOT.jar
WORKDIR /app

ENTRYPOINT ["java", "-jar", "trustedprofiles-1.0-SNAPSHOT.jar"]
