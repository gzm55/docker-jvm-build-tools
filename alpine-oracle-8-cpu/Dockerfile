FROM jeanblanchard/java:jdk-8u111

ENV MAVEN_VERSION=3.3.9 M2_HOME=/opt/maven \
    ANT_VERSION=1.10.0 ANT_HOME=/opt/ant \
    IVY_VERSION=2.4.0 \
    SBT_VERSION=0.13.13 SBT_HOME=/opt/sbt \
    PATH=$PATH:/opt/maven/bin:/opt/ant/bin:/opt/sbt/bin

RUN set -eux \
    && apk add --no-cache --virtual=.build-dependencies curl tar wget \

    ## Install maven at $M2_HOME
    && mkdir -p $M2_HOME \
    && curl -L https://www.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
     | tar xzf - -C $M2_HOME --strip-components=1 \
    && rm -rf $M2_HOME/bin/*.cmd \

    ## support maven-wrapper
    ## maintain two directory references for downloading from urls of maven central repos by maven-wrapper
    && mkdir -p /root/.m2/wrapper/dists/apache-maven-$MAVEN_VERSION-bin/2609u9g41na2l7ogackmif6fj2 \
    && ln -s $M2_HOME /root/.m2/wrapper/dists/apache-maven-$MAVEN_VERSION-bin/2609u9g41na2l7ogackmif6fj2/apache-maven-$MAVEN_VERSION \
    && mkdir -p /root/.m2/wrapper/dists/apache-maven-$MAVEN_VERSION-bin/2bef7dbss28mt21g2pltev5241 \
    && ln -s $M2_HOME /root/.m2/wrapper/dists/apache-maven-$MAVEN_VERSION-bin/2bef7dbss28mt21g2pltev5241/apache-maven-$MAVEN_VERSION \

    ## install maven extensions: takari-local-repository, takari-filemanager, takari-smart-builder
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/aether/takari-local-repository/0.11.2/takari-local-repository-0.11.2.jar \
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/takari-filemanager/0.8.3/takari-filemanager-0.8.3.jar \
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/maven/takari-smart-builder/0.4.1/takari-smart-builder-0.4.1.jar \

    ## Install ant at $ANT_HOME
    && mkdir -p $ANT_HOME \
    && curl -L https://www.apache.org/dist/ant/binaries/apache-ant-$ANT_VERSION-bin.tar.gz \
     | tar xzf - -C $ANT_HOME --strip-components=1 \
    && rm -rf $ANT_HOME/bin/*.cmd $ANT_HOME/bin/*.bat $ANT_HOME/manual \

    ## Install ivy at $ANT_HOME/lib
    && curl -L https://www.apache.org/dist/ant/ivy/$IVY_VERSION/apache-ivy-$IVY_VERSION-bin.tar.gz \
     | tar xzf - \
    && mv apache-ivy-$IVY_VERSION/ivy-$IVY_VERSION.jar $ANT_HOME/lib/ \
    && rm -rf apache-ivy-$IVY_VERSION \

    ## Install sbt at $SBT_HOME/lib, sbt launch scripts need bash
    ## use curl --insecure option to work round the buggy ca cert of bintray.com
    && apk add --no-cache bash \
    && mkdir -p $SBT_HOME \
    && curl -L --insecure -o sbt.tgz https://dl.bintray.com/sbt/native-packages/sbt/$SBT_VERSION/sbt-$SBT_VERSION.tgz \
    && echo "40d03d21a260c5a6a43f8349298f41c9d047f97972057d9d915afd8945faf979  sbt.tgz" \
     | sha256sum -c - \
    && tar xzf sbt.tgz -C $SBT_HOME --strip-components=1 \
    && rm -rf $SBT_HOME/bin/*.bat sbt.tgz \

    ## cleanup
    && apk del --no-cache .build-dependencies

VOLUME /root/.m2/repository /root/.ivy2 /root/.sbt
