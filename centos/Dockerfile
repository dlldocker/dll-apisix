FROM centos:7

MAINTAINER lcb "xinglou123@163.com"

ENV TZ "Asia/Shanghai"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ARG APISIX_VERSION=1.0
LABEL apisix_version="${APISIX_VERSION}"

RUN yum -y install yum-utils\
    && yum-config-manager --add-repo https://openresty.org/package/centos/openresty.repo \
	&& yum install -y openresty \
	&& yum install -y https://github.com/iresty/apisix/releases/download/$APISIX_VERSION/apisix-$APISIX_VERSION-0.el7.noarch.rpm \
	&& yum clean all

WORKDIR /usr/local/apisix

EXPOSE 9080 9443

CMD ["sh", "-c", "/usr/bin/apisix init && /usr/bin/apisix init_etcd && /usr/local/openresty/bin/openresty -p /usr/local/apisix -g 'daemon off;'"]

