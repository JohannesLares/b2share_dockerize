FROM elasticsearch:2.4.6
EXPOSE 9200 9300

RUN cd /usr/share/elasticsearch && \
    ./bin/plugin install -b mapper-attachments

RUN usermod -u 1000 elasticsearch && \
    groupmod -g 1000 elasticsearch && \
    chown -R elasticsearch.elasticsearch /usr/share/elasticsearch

CMD ["elasticsearch"]
