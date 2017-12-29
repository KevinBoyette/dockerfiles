FROM alpine:3.7

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go
ENV CONSUL_VERSION v1.0.2
ENV CONSUL_REPO 'https://github.com/hashicorp/consul'

# bash is needed by make  
RUN buildDependencies='bash go git gcc g++ libc-dev libgcc make  zip' \
    set -x \
    && apk --no-cache add --repository https://dl-3.alpinelinux.org/alpine/edge/community $buildDependencies \
    && mkdir -p mkdir -p /go/src/github.com/hashicorp /etc/consul.d \
    && git clone --depth 1 --branch ${CONSUL_VERSION} ${CONSUL_REPO} /go/src/github.com/hashicorp/consul \
    && cd /go/src/github.com/hashicorp/consul  \
    && XC_ARCH="amd64" XC_OS="linux" make all  \
    && mv bin/consul /usr/bin/ \
    && apk del $buildDependencies \
    && rm -rf /go 


ENTRYPOINT [ "consul" ]

