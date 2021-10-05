FROM registry.access.redhat.com/ubi8/s2i-core:1

ENV MAINTAINER="Aushacker <25114336+aushacker@users.noreply.github>" \
    MAVEN_OPTS="" \
    MAVEN_GOALS="package" \
    MAVEN_PHASES="" \
    S2I_JAVA_VERSION=1.0 \
    SUMMARY="An s2i builder image for assembling Java applications using Maven."

LABEL description=${SUMMARY} \
      io.k8s.description=${SUMMARY} \
      io.k8s.display-name="s2i-java 1.0.0" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.tags="builder,s2i-java,1.0.0" \
      maintainer=${MAINTAINER} \
      name="aushacker/s2i-java" \
      org.opencontainers.image.authors=${MAINTAINER} \
      summary=${SUMMARY}

RUN yum install -y --disableplugin=subscription-manager maven && \
    yum clean -y --disableplugin=subscription-manager all

COPY ./s2i/bin/ /usr/libexec/s2i

RUN chown -R 1001:1001 /opt/app-root

USER 1001

CMD ["/usr/libexec/s2i/usage"]
