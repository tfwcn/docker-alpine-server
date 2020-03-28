# 基于alpine的镜像
FROM alpine:3.9
MAINTAINER Docker PPHT <tfwcn@sina.cn>

#复制文件
COPY start.sh /root/start.sh
COPY supervisor.d/ /etc/supervisor.d

RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.9/main/" > /etc/apk/repositories \
	&& echo "http://mirrors.ustc.edu.cn/alpine/v3.9/community" >> /etc/apk/repositories \
	&& apk update \
	&& apk upgrade \
	&& apk add --no-cache bash bash-doc bash-completion \
	&& apk add --no-cache openssh-server openssh-sftp-server tzdata openrc supervisor \
	&& cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
	&& sed -i 's/#Port 22/Port 22/g' /etc/ssh/sshd_config \
	&& sed -i 's/#ListenAddress 0.0.0.0/ListenAddress 0.0.0.0/g' /etc/ssh/sshd_config \
	&& sed -i 's/#ListenAddress ::/ListenAddress ::/g' /etc/ssh/sshd_config \
	&& sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config \
	&& sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config \
	&& ssh-keygen -A \
	&& echo "root:123456" | chpasswd \
	&& chmod 777 /root/start.sh \
	&& rm -rf /var/cache/apk/*

# 开端口
EXPOSE 22
EXPOSE 9001

COPY supervisord.conf /etc/supervisord.conf

CMD "sh /root/start.sh"