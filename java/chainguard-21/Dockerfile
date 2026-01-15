FROM europe-north1-docker.pkg.dev/cgr-nav/pull-through/nav.no/jre:openjdk-21@sha256:acc858298f6437cece9f964eaf3cbfd1b17aa3fcfd43ae3d35fbb3e67518d317

ENV LANG='C.UTF-8' LANGUAGE='nb:en' LC_ALL='C.UTF-8' TZ="Europe/Oslo"

ENV JDK_JAVA_OPTIONS="-XX:+PrintCommandLineFlags \
                      -XX:ActiveProcessorCount=2 \
                      -XX:+UseParallelGC \
                      -XX:MaxRAMPercentage=75 \
                      -XX:-OmitStackTraceInFastThrow \
                      -Djava.security.egd=file:/dev/urandom \
                      -Duser.timezone=Europe/Oslo \
                      -Duser.language=nb \
                      -Duser.country=NO"

CMD ["-jar", "app.jar"]
