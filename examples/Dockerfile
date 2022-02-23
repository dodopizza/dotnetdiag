FROM golang:1.16-alpine as build
RUN apk --no-cache add ca-certificates

WORKDIR /build/

COPY go.mod go.sum /build/
RUN go mod download
COPY . /build
RUN go build -o tracing ./examples/tracing

FROM alpine:latest as run
RUN apk add --update --no-cache ca-certificates

COPY --from=build /build/tracing /go/bin/tracing

ENTRYPOINT [ "/go/bin/tracing" ]
