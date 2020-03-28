# 基于alpine的镜像
FROM highlevel/alpine-server:base
MAINTAINER Docker PPHT <tfwcn@sina.cn>

#复制文件
COPY glibc-2.29-r0.apk /root/glibc-2.29-r0.apk
COPY glibc-bin-2.29-r0.apk /root/glibc-bin-2.29-r0.apk
COPY glibc-i18n-2.29-r0.apk /root/glibc-i18n-2.29-r0.apk

RUN apk --no-cache add ca-certificates wget \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && apk add /root/glibc-2.29-r0.apk /root/glibc-bin-2.29-r0.apk /root/glibc-i18n-2.29-r0.apk \
	&& rm -rf /var/cache/apk/* /root/glibc-2.29-r0.apk /root/glibc-bin-2.29-r0.apk /root/glibc-i18n-2.29-r0.apk


# 开端口
EXPOSE 22
EXPOSE 9001

CMD /root/start.sh