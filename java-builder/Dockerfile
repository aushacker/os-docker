FROM registry.access.redhat.com/ubi8/ubi AS builder

RUN yum install -y --disableplugin=subscription-manager java-11-openjdk-devel && \
    yum install -y --disableplugin=subscription-manager git && \
    yum install -y --disableplugin=subscription-manager maven

RUN mvn --version

WORKDIR /tmp/build

RUN git clone https://github.com/aushacker/java-spi.git

WORKDIR /tmp/build/java-spi

RUN mvn package

FROM registry.access.redhat.com/ubi8/ubi

RUN yum install -y --disableplugin=subscription-manager java-11-openjdk && \
    yum clean -y --disableplugin=subscription-manager all

COPY --from=builder /tmp/build/java-spi/target/java-spi-0.0.1-SNAPSHOT-jar-with-dependencies.jar java-spi.jar

CMD java -jar java-spi.jar
