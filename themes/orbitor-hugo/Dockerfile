FROM nginx:alpine

ENV HUGO_VERSION="0.98.0"
ENV HUGO_ENV="dev"

USER root

RUN apk add --update \
    wget \
    git \
    ca-certificates

RUN wget --quiet https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    tar -xf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    chmod +x hugo && \
    mv hugo /usr/local/bin/hugo && \
    rm -rf hugo hugo_${HUGO_VERSION}_Linux-64bit.tar.gz

WORKDIR '/app'

COPY . .

RUN hugo -s . -e ${HUGO_ENV} -d /usr/share/nginx/html/

CMD nginx -g "daemon off;"