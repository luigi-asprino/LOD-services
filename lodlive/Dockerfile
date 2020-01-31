FROM nginx

ARG NAMESPACE_BASE
ARG SPARQL_ENDPOINT_URL

RUN apt-get update && \
	apt-get install --no-install-recommends --no-install-suggests -y git && \
	cd /opt && \
	git config --global http.sslverify false && \
	git clone https://github.com/stlab-istc-cnr/LodLive.git && \
	mv LodLive/* /usr/share/nginx/html/

#COPY lodlive.profile.js /usr/share/nginx/html/js/

COPY lodlive.profile_template.js /

RUN cat /lodlive.profile_template.js | \
    sed -e "s,NAMESPACE_BASE,${NAMESPACE_BASE},g" | \
    sed -e "s,SPARQL_ENDPOINT_URL,${SPARQL_ENDPOINT_URL},g"  \
    > /usr/share/nginx/html/js/lodlive.profile.js
