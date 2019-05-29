FROM alpine

# use aliyun mirror
RUN echo "https://mirrors.aliyun.com/alpine/latest-stable/main" > /etc/apk/repositories \
    && apk add --no-cache aria2
    
EXPOSE 6800

# should bind mount , download file saving path
VOLUME ["/dl"]

CMD ["aria2c", \
       "--dir=/dl", \
       "--max-connection-per-server=5", \
       "--enable-rpc=true", \
       "--rpc-allow-origin-all=true", \
       "--rpc-listen-all=true", \
       "--file-allocation=trunc", \
       "--continue=true"]
