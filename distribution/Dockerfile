FROM quay.io/keycloak/keycloak:15.0.2

ARG GIT_REPO
ARG GIT_BRANCH
ARG KEYCLOAK_DIST=file:///tmp/keycloak-15.0.4.tar.gz

ENV JBOSS_HOME=/opt/jboss/keycloak
ENV JDBC_MARIADB_VERSION=2.5.4
ENV JDBC_MSSQL_VERSION=8.2.2.jre11
ENV JDBC_MYSQL_VERSION=8.0.22
ENV JDBC_POSTGRES_VERSION=42.2.5
ENV KEYCLOAK_VERSION=15.0.4
ENV LANG=en_US.UTF-8
ENV LAUNCH_JBOSS_IN_BACKGROUND=1
ENV PROXY_ADDRESS_FORWARDING=false

USER root

COPY ./server-dist/target/keycloak-15.0.4.tar.gz /tmp/keycloak-15.0.4.tar.gz

RUN microdnf update -y && \
    microdnf install -y glibc-langpack-en gzip hostname java-11-openjdk-headless openssl tar which && \
    microdnf clean all && \
    rm -r /opt/jboss/keycloak && \
    sh /opt/jboss/tools/build-keycloak.sh

USER 1000

EXPOSE 8080
EXPOSE 8443

ENTRYPOINT ["/opt/jboss/tools/docker-entrypoint.sh"]

CMD ["-b", "0.0.0.0"]
