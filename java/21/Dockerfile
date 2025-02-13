FROM eclipse-temurin:21.0.5_11-jre-alpine
LABEL org.opencontainers.image.source=https://github.com/navikt/sif-baseimage-java
ARG CACHEBUST=1
RUN apk update \
    && apk upgrade \
    && apk add --no-cache dumb-init musl-locales \
    && sed -i '/nb_NO.UTF-8/s/^# //' /etc/apk/world \
    && echo "export LANG=nb_NO.UTF-8" >> /etc/profile \
    && echo "export LC_ALL=nb_NO.UTF-8" >> /etc/profile \
    && umask o+r \
    && addgroup -S -g 1069 apprunner \
    && adduser -S -u 1069 --ingroup apprunner --no-create-home apprunner

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV DEFAULT_JVM_OPTS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=2 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"
#init-scripts
COPY ../scripts /

WORKDIR /app
USER apprunner
EXPOSE 8080
ENTRYPOINT ["dumb-init", "--", "/entrypoint.sh"]


