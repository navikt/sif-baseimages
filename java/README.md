# Java-baseimage (Chainguard)

`ghcr.io/navikt/sif-baseimages/java-chainguard-25` bygger på Navs Chainguard-JRE (`cgr-nav/.../jre:openjdk-25`). Imaget har ikke shell, og JVM-en kjører som PID 1.

## Bruk

```Dockerfile
FROM ghcr.io/navikt/sif-baseimages/java-chainguard-25:<tag>
LABEL org.opencontainers.image.source=https://github.com/navikt/<repo>

WORKDIR /app
COPY target/app.jar app.jar
```

Imaget starter med `java -jar app.jar` fra arbeidsmappen. Bruk en tidsstempel-tag (for eksempel `2026.11.19.0715Z`), ikke `latest`.

## JVM-opsjoner

Imaget setter `JDK_JAVA_OPTIONS` med standardvalg (minne, GC, tidssone og språk). Ikke overstyr den i Nais-manifestet. Legg ekstra opsjoner i `JAVA_TOOL_OPTIONS`. JVM-en leser begge.

Eksempler på opsjoner i `JAVA_TOOL_OPTIONS`:

- Webproxy i FSS (apper med `webproxy: true`): `$(JAVA_PROXY_OPTIONS)`
- Remote debug: `-agentlib:jdwp=...`

```yaml
env:
  - name: JAVA_TOOL_OPTIONS
    value: $(JAVA_PROXY_OPTIONS)
```

## Oppdatering

`FROM` er låst til en digest. [Navs digestabot](https://sikkerhet.nav.no/docs/verktoy/chainguard-dockerimages#digestabot) (`.github/workflows/digestabot.yml`) sjekker hver natt om taggen har fått ny digest, og lager i så fall en PR. Når PR-en er merget, bygger `build.yml` et nytt image med ny tidsstempel-tag. Appene må selv bumpe taggen.

Dependabot brukes ikke for Chainguard-images, fordi den ville byttet til en ny Java-versjon.

## Ny Java-versjon

1. Kopier `java/chainguard-25` til for eksempel `java/chainguard-26`, og bytt taggen i `FROM` til `jre:openjdk-26` med digest.
2. Legg `'chainguard-26'` til i matrisen i `.github/workflows/build.yml`. Imaget blir `java-chainguard-26`.
3. Kopier jobben `digest-update-chainguard-25` i `digestabot.yml`, og bytt `working-dir` og `branch-for-pr`.
4. Legg versjonen til i matrisene i `trivy.yml` og `package_cleanup.yml`.
