FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-25@sha256:2c799fa168bfa527884e8ae5a14ad3d46a6919d37185ca2466eead6eb1e76d1e

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
