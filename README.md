# docker-jvm-build-tools
Docker images with common java building tools.

Current Version
--
0.2.0

Base Images
--

- alpine 3.5 + oracle jdk 8 (cpu) 8u111
- alpine 3.5 + oracle jdk 8 psu 8u112

Compoments
--

### OS + JDK
- alpine (3.5) + oracle jdk (8u111, 8u112) + dependent glibc 2.23-r3

### building tools
- maven 3.3.9
- maven extension
  - takari-local-repository 0.11.2
  - takari-filemanager 0.8.3
  - takari-smart-builder 0.4.1
- ant 1.10.0
- ivy 2.4.0
- sbt 0.13.13 (depend on bash, not bootstrap)

Supported Tags
--

Every tag is in the form of  `<collect-version>[-<OS-and-JDK-base>]`. If `<collect-version>` is `latest`,
it is build from the master branch; if `<collect-version>` is a real sematic version,
it is build from release tags.

- latest
- latest-alpine-oracle-8
- latest-alpine-oracle-8-psu

Volumes
--

- /root/.m2/repository
- /root/.ivy2
- /root/.sbt
