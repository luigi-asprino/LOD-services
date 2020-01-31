FROM  maven:3.6.3-jdk-8

RUN cd /opt && \
	git clone https://github.com/stlab-istc-cnr/LODE.git

WORKDIR /opt/LODE

EXPOSE 8080

ENTRYPOINT ["mvn", "clean", "jetty:run"]