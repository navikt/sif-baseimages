# Java-baseimage (Chainguard)

`ghcr.io/navikt/sif-baseimages/java-chainguard-25` bygger på Navs Chainguard-JRE (`cgr-nav/.../jre:openjdk-25`). Imaget har ikke shell, init-skript eller entrypoint-skript. JVM-en kjører som PID 1.

## Bruk

```Dockerfile
FROM ghcr.io/navikt/sif-baseimages/java-chainguard-25:<tag>
LABEL org.opencontainers.image.source=https://github.com/navikt/<repo>

WORKDIR /app
COPY target/app.jar app.jar
```

Imaget starter med `java -jar app.jar` fra arbeidsmappen. Bruk en tidsstempel-tag (for eksempel `2026.11.19.0715Z`), ikke `latest`.

## JVM-opsjoner

Imaget setter `JDK_JAVA_OPTIONS` med standardvalg (minne, GC, tidssone og språk). Ikke overstyr `JDK_JAVA_OPTIONS` i Nais-manifestet. Legg ekstra opsjoner i `JAVA_TOOL_OPTIONS`. JVM-en leser begge.

## Webproxy i FSS

Init-skriptet som satte proxy finnes ikke lenger. Apper med `webproxy: true` må sette proxy selv:

```yaml
env:
  - name: JAVA_TOOL_OPTIONS
    value: $(JAVA_PROXY_OPTIONS)
```

## Erstatning for de gamle init-skriptene

- **Vault-filer** (`/var/run/secrets/nais.io/vault/*.env`) blir ikke lenger lest inn som miljøvariabler. Sett verdiene i manifestet, eller les filene fra appen.
- **Truststore:** Trenger appen Navs truststore, legg `-Djavax.net.ssl.trustStore=$(NAV_TRUSTSTORE_PATH) -Djavax.net.ssl.trustStorePassword=$(NAV_TRUSTSTORE_PASSWORD)` i `JAVA_TOOL_OPTIONS`.
- **Azure-filer:** Nais setter `AZURE_*` som miljøvariabler, så filene trenger ikke leses inn.
- **Remote debug:** Legg `-agentlib:jdwp=...` i `JAVA_TOOL_OPTIONS` ved behov.

## Oppdatering

`FROM` i hver Dockerfile er låst til en digest. Workflowen `.github/workflows/digestabot.yml` bruker [Navs digestabot](https://sikkerhet.nav.no/docs/verktoy/chainguard-dockerimages#digestabot) og kjører hver natt kl. 00:00 UTC, og kan også startes manuelt. Den logger inn i `cgr-nav`-registryet som teamet og sjekker om taggen (for eksempel `jre:openjdk-25`) har fått ny digest. I så fall lager den en PR med ny digest på branchen `update-chainguard-25-image`.

Når PR-en er merget, bygger `build.yml` et nytt image med ny tidsstempel-tag. Appene må deretter bumpe taggen sin selv.

Dependabot kan ikke brukes for Chainguard-images. Den ser bare etter nyere tagger og ville byttet til en ny Java-versjon. Selve digestabot-actionen er låst til en SHA og oppdateres av Dependabot for github-actions.

## Ny Java-versjon

1. Kopier `java/chainguard-25` til for eksempel `java/chainguard-26`, og bytt taggen i `FROM` til `jre:openjdk-26` med digest.
2. Legg `'chainguard-26'` til i matrisen i `.github/workflows/build.yml`. Imaget blir `java-chainguard-26`.
3. Kopier jobben `digest-update-chainguard-25` i `digestabot.yml`, og bytt `working-dir` og `branch-for-pr`.
4. Legg versjonen til i matrisene i `trivy.yml` og `package_cleanup.yml`.
