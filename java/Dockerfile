FROM gurimusan/nvim:latest

MAINTAINER gurimusan <gurimusan@gmail.com>

USER root

ENV LANG ja_JP.UTF-8
ENV TIMEZONE Asia/Tokyo
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

RUN set -x && apk add --no-cache openjdk8 apache-ant \
    && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" -o /tmp/jce_policy-8.zip "http://download.oracle.com/otn-pub/java/jce/8/jce_policy-8.zip" \
    && cd /tmp \
    && unzip jce_policy-8.zip \
    && mv UnlimitedJCEPolicyJDK8/US_export_policy.jar $JAVA_HOME/jre/lib/security/US_export_policy.jar \
    && mv UnlimitedJCEPolicyJDK8/local_policy.jar $JAVA_HOME/jre/lib/security/local_policy.jar \
    && rm -Rf UnlimitedJCEPolicy \
    && rm -Rf jce_policy-8.zip.zip \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

RUN cd /usr/lib && \
    wget https://downloads.gradle.org/distributions/gradle-3.3-bin.zip &&\
    unzip "gradle-3.3-bin.zip" && \
    ln -s "/usr/lib/gradle-3.3/bin/gradle" /usr/bin/gradle && \
    rm "gradle-3.3-bin.zip"

USER gurimusan
WORKDIR /home/gurimusan

CMD ["/bin/zsh"]
