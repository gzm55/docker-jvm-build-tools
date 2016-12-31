# docker-jvm-build-tools
Docker images with common java building tools.

Current Version
--
0.1.x

Base Images
--

- alpine 3.4 + oracle cpu jdk 8u111
- alpine 3.4 + oracle psu jdk 8u112

Compoments
--

### OS + JDK
- alpine (3.4) + oracle jdk (8u111, 8u112) + dependent glibc 2.23-r3

### building tools
- maven 3.3.9
- maven extension
  - takari-local-repository 0.11.2
  - takari-filemanager 0.8.3
  - takari-smart-builder 0.4.1
- ant 1.9.7
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
