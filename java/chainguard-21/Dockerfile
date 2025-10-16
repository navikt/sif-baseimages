FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-21@sha256:c8b96de1eaffde9007417116e04569831c5c34965c321407f9e4c109cf7589c2

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=2 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"

CMD ["-jar", "app.jar"]
