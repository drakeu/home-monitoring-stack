FROM alpine:3.5

RUN apk update && apk add python curl
RUN mkdir /apps
RUN curl -Lo speedtest-cli https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py && mv /speedtest-cli /apps && chmod +x /apps/speedtest-cli

ADD crontab/3min /etc/periodic/3min
RUN chmod 755 /etc/periodic/3min/*

RUN crontab -l | { cat; echo "*/3    *       *       *       *       run-parts /etc/periodic/3min"; } | crontab -

CMD ["crond", "-f", "-d", "8"]
