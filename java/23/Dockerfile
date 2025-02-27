ARG BASE_IMAGE_VERSION
FROM eclipse-temurin:23.0.2_7-jdk-alpine AS builder

WORKDIR /builder
#bygg egen java runtime, tar her med alle moduler som er med i jre-bygget for eclipse temurin. Disse kan finnes ved å kjøre 'java --list-modules' et sted man har jre-bygget

#for 21
#RUN jlink --add-modules java.base,java.compiler,java.datatransfer,java.desktop,java.instrument,java.logging,java.management,java.management.rmi,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.se,java.security.jgss,java.security.sasl,java.smartcardio,java.sql,java.sql.rowset,java.transaction.xa,java.xml,java.xml.crypto,jdk.accessibility,jdk.charsets,jdk.crypto.cryptoki,jdk.crypto.ec,jdk.dynalink,jdk.httpserver,jdk.incubator.vector,jdk.internal.vm.ci,jdk.internal.vm.compiler,jdk.internal.vm.compiler.management,jdk.jdwp.agent,jdk.jfr,jdk.jsobject,jdk.localedata,jdk.management,jdk.management.agent,jdk.management.jfr,jdk.naming.dns,jdk.naming.rmi,jdk.net,jdk.nio.mapmode,jdk.sctp,jdk.security.auth,jdk.security.jgss,jdk.unsupported,jdk.xml.dom,jdk.zipfs \
#    --strip-debug --no-man-pages --no-header-files --compress=1 --output javaruntime


RUN jlink --add-modules java.base,java.compiler,java.datatransfer,java.desktop,java.instrument,java.logging,java.management,java.management.rmi,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.se,java.security.jgss,java.security.sasl,java.smartcardio,java.sql,java.sql.rowset,java.transaction.xa,java.xml,java.xml.crypto,jdk.accessibility,jdk.charsets,jdk.crypto.cryptoki,jdk.dynalink,jdk.graal.compiler,jdk.graal.compiler.management,jdk.httpserver,jdk.incubator.vector,jdk.internal.vm.ci,jdk.jdwp.agent,jdk.jfr,jdk.jsobject,jdk.localedata,jdk.management,jdk.management.agent,jdk.management.jfr,jdk.naming.dns,jdk.naming.rmi,jdk.net,jdk.nio.mapmode,jdk.sctp,jdk.security.auth,jdk.security.jgss,jdk.unsupported,jdk.xml.dom,jdk.zipfs \
    --strip-debug --no-man-pages --no-header-files --compress=1 --output javaruntime

FROM ghcr.io/navikt/sif-baseimages/java-base:${BASE_IMAGE_VERSION:-"latest"}


LABEL org.opencontainers.image.source=https://github.com/navikt/sif-baseimages/java-23

COPY --from=builder /builder/javaruntime /opt/java/openjdk
