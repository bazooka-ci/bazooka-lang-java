FROM debian:jessie

ENV JAVA_VERSION 7

# Install Java
RUN \
    echo oracle-java$JAVA_VERSION-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
    apt-get update && \
    apt-get -y install augeas-tools curl oracle-java$JAVA_VERSION-installer oracle-java$JAVA_VERSION-unlimited-jce-policy && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-$JAVA_VERSION-oracle

ENV GRADLE_VERSION 2.10
ENV MAVEN_VERSION 3.3.9
ENV ANT_VERSION 1.9.6

RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

RUN cd /usr/share \
	&& wget -q https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-all.zip \
	&& unzip -q gradle-$GRADLE_VERSION-all.zip \
	&& mv /usr/share/gradle-$GRADLE_VERSION /usr/share/gradle \
	&& ln -s /usr/share/gradle/bin/gradle /usr/bin/gradle \
	&& rm gradle-$GRADLE_VERSION-all.zip

RUN curl -fsSL http://www.us.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz | tar xzf - -C /usr/share \
    && mv /usr/share/apache-ant-${ANT_VERSION} /usr/share/ant \
    && ln -s /usr/share/ant/bin/ant /usr/bin/ant

# Set Appropriate Environmental Variables
ENV GRADLE_HOME /usr/share/gradle
ENV MAVEN_HOME /usr/share/maven
ENV ANT_HOME /usr/share/ant
