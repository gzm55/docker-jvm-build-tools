# docker-jvm-build-tools
Docker images with common java building tools.

Current Version
--
0.4.0

Base Images
--

- alpine 3.5 + oracle jdk 8 8u131

Compoments
--

### OS + JDK
- alpine (3.5) + oracle jdk (8u131) + dependent glibc 2.25-r0

### building tools
- maven 3.5.0
- maven extension
  - takari-local-repository 0.11.2
  - takari-filemanager 0.8.3
  - takari-smart-builder 0.6.0
- ant 1.10.1
- ivy 2.4.0
- sbt 0.13.15 (depend on bash, not bootstrap)

Supported Tags
--

Every tag is in the form of  `<collect-version>[-<OS-and-JDK-base>]`. If `<collect-version>` is `latest`,
it is build from the master branch; if `<collect-version>` is a real sematic version,
it is build from release tags.

- latest
- latest-alpine-oracle-8
- 0.4
- 0.4-alpine-oracle-8
- 0.3
- 0.3-alpine-oracle-8

Volumes
--

- /root/.m2/repository
- /root/.ivy2
- /root/.sbt
