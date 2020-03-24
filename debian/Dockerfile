FROM debian:buster-slim

ENV FAH_VERSION_MINOR=7.5.1
ENV FAH_VERSION_MAJOR=7.5

# https://foldingforum.org/viewtopic.php?f=106&t=30836&sid=6c39de1dc08757c468f533d41a20bc16&start=15#p313509
# https://github.com/FoldingAtHome/fah-issues/issues/1246
RUN apt-get update &&\
    apt-get install --no-install-recommends -y wget ocl-icd-opencl-dev &&\
    wget --no-check-certificate https://download.foldingathome.org/releases/public/release/fahclient/debian-stable-64bit/v${FAH_VERSION_MAJOR}/fahclient_${FAH_VERSION_MINOR}_amd64.deb &&\
    apt-get remove -y wget &&\
    apt-get autoremove -y &&\
    dpkg -x fahclient_${FAH_VERSION_MINOR}_amd64.deb / &&\
    apt-get clean &&\
    rm -rfv /var/lib/apt/lists/* /tmp/* /var/log/* &&\
    mkdir -p /etc/fahclient/ &&\
    chown -R 65534:65534 /etc/fahclient/
# touch /etc/fahclient/config.xml

USER 65534:65534

WORKDIR /etc/fahclient

EXPOSE 7396 36330

ENTRYPOINT ["/usr/bin/FAHClient", "--data-directory=/etc/fahclient"]

CMD ["--fold-anon=true", "--gui-enabled=false", "--run-as=nobody"]