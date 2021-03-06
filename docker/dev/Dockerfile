# Dockerfile for making Algernon serve HTTP on port 3000, in development mode

FROM golang:alpine
MAINTAINER Alexander F Rødseth <xyproto@archlinux.org>

RUN apk update && apk add bash curl git mercurial go openssh-client && rm -rf /var/cache/apk/*
# apk add subversion bzr ca-certificates

RUN mkdir -p /go/src /go/bin && chmod -R 777 /go
ENV GOPATH /go
ENV PATH /go/bin/:$PATH

ENV CGO_ENABLED=0
RUN go get github.com/xyproto/algernon
RUN ln -s "$GOPATH/bin/algernon" /usr/bin/algernon

VOLUME /srv/algernon
VOLUME /etc/algernon

WORKDIR /srv/algernon

# -c assumes no files will be added or removed, for a slight increase in speed
# --domain makes Algernon look for a folder named the same as the domain it serves
# --server turns off interactive and debug mode
# --cachesize sets a file cache size, in bytes
# --prod makes Algernon serve HTTP on port 80 and HTTPS+HTTP/2 on port 443
# --cert and --key is for setting the HTTPS certificate
#
# Other parameters that might be of interest is "--addr", ":3000" together with
# "--server" but without "--prod" for serving only HTTP on port 3000
#
# "--log", "/var/log/algernon.log" can be used for logging errors
#
# "--dev" enables debug mode, uses regular HTTP, enables Bolt and sets the cache mode to "dev".
# "--autorefresh" enables the autorefresh feature where pages are refreshed upon file save.
#
# The final parameter is the directory to serve, for instance /srv/algernon
#
CMD ["algernon", "--domain", "--server", "--dev", "--autorefresh"]

EXPOSE 3000
