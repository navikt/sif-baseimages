FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-25@sha256:c84b8253eae65f7ee3ff0db63e6b25316efd29801b63c8bbc9facc6ef722b866

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=4 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"

CMD ["-jar", "app.jar"]
