FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-25@sha256:5aad9914e9e0ee259f380c37d3867f8ae87d78d9950e400ba42abf60dde7016e

ENV LANG='nb_NO.UTF-8' LANGUAGE='nb_NO:nb' LC_ALL='nb_NO.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=4 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo"

CMD ["-jar", "app.jar"]
