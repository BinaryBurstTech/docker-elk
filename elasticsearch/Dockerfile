ARG ELASTIC_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:${ELASTIC_VERSION:-8.17.4}

# Přidání konfiguračního souboru do nového umístění
COPY config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml.custom

# Upravení entrypointu pro použití vlastní konfigurace
RUN echo '#!/bin/bash\ncp /usr/share/elasticsearch/config/elasticsearch.yml.custom /usr/share/elasticsearch/config/elasticsearch.yml\nexec /usr/local/bin/docker-entrypoint.sh "$@"' > /usr/local/bin/custom-entrypoint.sh \
    && chmod +x /usr/local/bin/custom-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/custom-entrypoint.sh"]
CMD ["elasticsearch"]