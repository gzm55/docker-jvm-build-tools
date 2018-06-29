FROM jeanblanchard/java:jdk-8u171

ENV MAVEN_VERSION=3.5.4 M2_HOME=/opt/maven \
    ANT_VERSION=1.10.4 ANT_HOME=/opt/ant \
    IVY_VERSION=2.4.0 \
    SBT_VERSION=1.1.6 SBT_HOME=/opt/sbt \
    PATH=$PATH:/opt/maven/bin:/opt/ant/bin:/opt/sbt/bin

RUN set -eux \
    && apk add --no-cache --virtual=.build-dependencies curl tar wget \

    ## Install maven at $M2_HOME
    && mkdir -p $M2_HOME \
    && curl -L https://www.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
     | tar xzf - -C $M2_HOME --strip-components=1 \
    && rm -rf $M2_HOME/bin/*.cmd \

    ## install maven extensions: takari-local-repository, takari-filemanager, takari-smart-builder
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/aether/takari-local-repository/0.11.2/takari-local-repository-0.11.2.jar \
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/takari-filemanager/0.8.3/takari-filemanager-0.8.3.jar \
    && wget -P $M2_HOME/lib/ext https://repo.maven.apache.org/maven2/io/takari/maven/takari-smart-builder/0.6.1/takari-smart-builder-0.6.1.jar \

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
    && apk add --no-cache bash \
    && mkdir -p $SBT_HOME \
    && curl -L https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz \
     | tar xzf - -C $SBT_HOME --strip-components=1 \
    && rm -rf $SBT_HOME/bin/*.bat $SBT_HOME/lib/local-preloaded sbt.tgz \

    ## cleanup
    && apk del --no-cache .build-dependencies

VOLUME /root/.m2/repository /root/.m2/wrapper /root/.ivy2 /root/.sbt
