FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-25@sha256:59a5bc362a0372cc1ba4113ffabe0c689ac42a744a8d1aca38b8109920aa64fa

ENV LANG='C.UTF-8' LANGUAGE='nb:en' LC_ALL='C.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=4 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo \
                      -Duser.language=nb \
                      -Duser.country=NO"

CMD ["-jar", "app.jar"]
