FROM maven:3.5.0-jdk-8 as lodview

ARG SPARQL_ENDPOINT_URL
ARG SPARQL_ENDPOINT_TYPE
ARG NAMESPACE
ARG LODLIVE_URL

#RUN echo "NAMESPACE arg: ${NAMESPACE}" && \
#    echo "LODLIVE_URL arg ${LODLIVE_URL}" && \
#    echo "SPARQL_ENDPOINT_TYPE arg ${SPARQL_ENDPOINT_TYPE}" && \
#    echo "SPARQL_ENDPOINT_URL arg ${SPARQL_ENDPOINT_URL}"

RUN apt-get update \
    && apt-get install -y git

RUN git clone https://github.com/stlab-istc-cnr/LodView.git

COPY conf_template.ttl /

RUN cat /conf_template.ttl | \
    sed -e "s,LODLIVE_URL,${LODLIVE_URL},g" | \
    sed -e "s,SPARQL_ENDPOINT_URL,${SPARQL_ENDPOINT_URL},g" | \
    sed -e "s,SPARQL_ENDPOINT_TYPE,${SPARQL_ENDPOINT_TYPE},g" | \
    sed -e "s,NAMESPACE,${NAMESPACE},g" \
    > /LodView/src/main/webapp/WEB-INF/conf.ttl

# COPY conf.ttl /LodView/src/main/webapp/WEB-INF/

RUN cd LodView \
  && mvn compile war:war

FROM tomcat:7
COPY --from=lodview /LodView/target/lodview.war /usr/local/tomcat/webapps/
