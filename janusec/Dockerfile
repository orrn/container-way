FROM ubuntu:22.04 as Build
ENV OS_ARCH="${TARGETARCH:-amd64}" \
    OS_NAME="linux" \
    APP_VERSION='1.2.9'
RUN apt update && \
    apt install wget -y
RUN wget https://github.com/Janusec/Application-Gateway/releases/download/v${APP_VERSION}/janusec-${APP_VERSION}-${OS_ARCH}.tar.gz -O /tmp/janusec.tar.gz \
    && tar -zxvf /tmp/janusec.tar.gz -C /tmp/ \
    && mv /tmp/janusec-${APP_VERSION}-${OS_ARCH} /tmp/janusec \
    && mkdir -p /tmp/janusec/log
COPY config.json /tmp/janusec/config.json

FROM ubuntu:22.04 as Image
ENV APP_VERSION="v1.2.9" \
    TZ=Asia/Shanghai
WORKDIR /
LABEL work.amap.image.description="Application packaged by orrn" \
      work.amap.image.version="v1.2.9" \
      work.amap.image.source="https://github.com/Janusec/Application-Gateway"
RUN apt-get update -y \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "${TZ}" > /etc/timezone \
    && apt install -y tzdata \
    && rm -rf /var/lib/apt/lists/*
COPY --from=Build /tmp/janusec /janusec
CMD ["/janusec/janusec"]
