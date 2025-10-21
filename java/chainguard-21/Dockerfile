FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-21@sha256:71f40e0718ad8425d20248777790a4840e1e357af799ab8f2a2b43912d32ddfb

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=2 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"

CMD ["-jar", "app.jar"]
