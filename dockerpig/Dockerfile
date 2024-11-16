FROM golang:1.16.15

RUN mkdir /src
WORKDIR /src

COPY ./go.mod .
COPY ./go.sum .

RUN go mod download

COPY ./ .

RUN go build

FROM alpine:latest

RUN apk add libc6-compat
RUN mkdir /app
RUN mkdir /app/resources
WORKDIR /app

COPY --from=0 /src/pig .
COPY --from=0 /src/resources/index.html ./resources/

EXPOSE 8000

RUN ["chmod", "+x", "/app/pig"]
CMD ["/app/pig"]
