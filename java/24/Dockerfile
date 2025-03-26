ARG BASE_IMAGE_VERSION
FROM eclipse-temurin:24_36-jdk-alpine AS builder
WORKDIR /builder
#bygg egen java runtime, tar her med alle moduler som er med i jre-bygget for eclipse temurin. Disse kan finnes ved å kjøre 'java --list-modules' et sted man har jre-bygget
# har tatt bort jdk.incubator.vector, da vi normalt ikke bruker incubator-features
#et alternativ til å bygge med jlink, er å ha avhengighet til eclipse-temurin<versjon>-jre-alpine, og kopiere /opt/java/openjdk derfra. Fordelen med jlink er at vi kan fjerne moduler vi ikke trenger, og mulighet til å justere argumenter compress.

RUN jlink --add-modules java.base,java.compiler,java.datatransfer,java.desktop,java.instrument,java.logging,java.management,java.management.rmi,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.se,java.security.jgss,java.security.sasl,java.smartcardio,java.sql,java.sql.rowset,java.transaction.xa,java.xml,java.xml.crypto,jdk.accessibility,jdk.charsets,jdk.crypto.cryptoki,jdk.dynalink,jdk.graal.compiler,jdk.graal.compiler.management,jdk.httpserver,jdk.internal.vm.ci,jdk.jdwp.agent,jdk.jfr,jdk.jsobject,jdk.localedata,jdk.management,jdk.management.agent,jdk.management.jfr,jdk.naming.dns,jdk.naming.rmi,jdk.net,jdk.nio.mapmode,jdk.sctp,jdk.security.auth,jdk.security.jgss,jdk.unsupported,jdk.xml.dom,jdk.zipfs \
    --strip-debug --no-man-pages --no-header-files --compress=1 --output javaruntime



FROM ghcr.io/navikt/sif-baseimages/java-base:${BASE_IMAGE_VERSION:-"latest"}
LABEL org.opencontainers.image.source=https://github.com/navikt/sif-baseimages/java-24
COPY --from=builder /builder/javaruntime /opt/java/openjdk




