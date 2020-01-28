FROM tenforce/virtuoso:virtuoso7.2.5

# COPY data
#COPY data.nt /usr/local/virtuoso-opensource/var/lib/virtuoso/db/toLoad/data.nt
#COPY data.nt /toLoad/data.nt
COPY toLoad /toLoad

# Add Virtuoso config
COPY virtuoso.ini /virtuoso.ini

RUN echo "mv /toLoad /data && sh /virtuoso.sh " > "/start.sh"

CMD ["/bin/bash", "/start.sh"]
