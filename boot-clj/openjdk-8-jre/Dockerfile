FROM ajchemist/openjdk:8u162
MAINTAINER aJchemist "ajchemist@turingmind.com"

ARG BOOT_VERSION=2.7.2
ARG BOOT_CHECKSUM=f717ef381f2863a4cad47bf0dcc61e923b3d2afb

ENV BOOT_VERSION=${BOOT_VERSION}
ENV BOOT_INSTALL=/usr/local/bin

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl

RUN mkdir -p $BOOT_INSTALL \
    && curl -Lo $BOOT_INSTALL/boot https://github.com/boot-clj/boot-bin/releases/download/${BOOT_VERSION}/boot.sh \
    && echo "Comparing installer checksum..." \
    && echo "${BOOT_CHECKSUM} *$BOOT_INSTALL/boot" | sha1sum -c - \
    && chmod +x $BOOT_INSTALL/boot;

ENV PATH=$PATH:$BOOT_INSTALL
ENV BOOT_AS_ROOT=yes
ENV BOOT_EMIT_TARGET=no
ENV BOOT_CLOJURE_NAME=org.clojure/clojure
ENV BOOT_HOME=/.boot
ENV BOOT_LOCAL_REPO=/m2/repository
ENV BOOT_JVM_OPTIONS="-XX:+TieredCompilation -XX:TieredStopAtLevel=1 -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xverify:none"

# download & install deps, cache REPL and web deps
# RUN /usr/bin/boot web -s doesnt/exist repl -e '(System/exit 0)' && rm -rf target

ENTRYPOINT ["boot"]
