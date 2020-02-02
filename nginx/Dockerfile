FROM nginx:1.17.7

ARG EXTERNAL_HOSTNAME
ARG NAMESPACE_BASE

COPY index_template.html /

RUN mkdir /usr/share/nginx/html/yasgui && \
	cat /index_template.html | \
    sed -e "s,EXTERNAL_HOSTNAME,${EXTERNAL_HOSTNAME},g"  \
    > /usr/share/nginx/html/yasgui/index.html

COPY nginx.conf /etc/nginx/nginx.conf

RUN apt-get update && \
	apt-get install --no-install-recommends --no-install-suggests -y git && \
	cd /opt && \
	git config --global http.sslverify false && \
	git clone https://github.com/stlab-istc-cnr/LodLive.git && \
	mkdir /usr/share/nginx/html/lodlive && \ 
	mv LodLive/* /usr/share/nginx/html/lodlive/

COPY lodlive.profile_template.js /

RUN cat /lodlive.profile_template.js | \
    sed -e "s,NAMESPACE_BASE,${NAMESPACE_BASE},g" | \
    sed -e "s,EXTERNAL_HOSTNAME,${EXTERNAL_HOSTNAME},g"  \
    > /usr/share/nginx/html/lodlive/js/lodlive.profile.js

