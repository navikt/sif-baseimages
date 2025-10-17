FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-21@sha256:e5a35cbddc2b65fe04887b8924c89af79a2c5e26221191a95e1b3ba9c2c03c18

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=2 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"

CMD ["-jar", "app.jar"]
