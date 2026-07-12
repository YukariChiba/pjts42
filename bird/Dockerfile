FROM alpine:latest

RUN apk add --no-cache bird2

CMD [ "bird", "-d", "-s", "/run/bird.ctl", "-c", "/etc/bird.conf" ]
