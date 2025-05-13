ARG BASE_IMAGE_VERSION
FROM eclipse-temurin:11.0.16_8-jdk-alpine AS builder
WORKDIR /builder
#bygg egen java runtime, tar her med alle moduler som er med i jre-bygget for eclipse temurin. Disse kan finnes ved å kjøre 'java --list-modules' et sted man har jre-bygget
#et alternativ til å bygge med jlink, er å ha avhengighet til eclipse-temurin<versjon>-jre-alpine, og kopiere /opt/java/openjdk derfra. Fordelen med jlink er at vi kan fjerne moduler vi ikke trenger, og mulighet til å justere argumenter compress.
RUN jlink --add-modules java.basej,java.compilerj,java.datatransferj,java.desktopj,java.instrumentj,java.loggingj,java.managementj,java.management.rmij,java.namingj,java.net.httpj,java.prefsj,java.rmij,java.scriptingj,java.sej,java.security.jgssj,java.security.saslj,java.smartcardioj,java.sqlj,java.sql.rowsetj,java.transaction.xaj,java.xmlj,java.xml.cryptoj,jdk.accessibilityj,jdk.aotj,jdk.charsetsj,jdk.crypto.cryptokij,jdk.crypto.ecj,jdk.dynalinkj,jdk.httpserverj,jdk.internal.edj,jdk.internal.lej,jdk.internal.vm.cij,jdk.internal.vm.compilerj,jdk.internal.vm.compiler.managementj,jdk.jdwp.agentj,jdk.jfrj,jdk.jsobjectj,jdk.localedataj,jdk.managementj,jdk.management.agentj,jdk.management.jfrj,jdk.naming.dnsj,jdk.naming.ldapj,jdk.naming.rmij,jdk.netj,jdk.packj,jdk.scripting.nashornj,jdk.scripting.nashorn.shellj,jdk.sctpj,jdk.security.authj,jdk.security.jgssj,jdk.unsupportedj,jdk.xml.domj,jdk.zipfsj \
    --strip-debug --no-man-pages --no-header-files --compress=1 --output javaruntime



FROM ghcr.io/navikt/sif-baseimages/java-base:${BASE_IMAGE_VERSION:-"latest"}
LABEL org.opencontainers.image.source=https://github.com/navikt/sif-baseimages/java-11
COPY --from=builder /builder/javaruntime /opt/java/openjdk

