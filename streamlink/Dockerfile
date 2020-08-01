FROM rayou/streamlink:latest
RUN apk add -U tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && apk del tzdata
ENTRYPOINT ["/bin/sh"]
