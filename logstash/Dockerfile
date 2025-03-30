ARG ELASTIC_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/logstash/logstash:${ELASTIC_VERSION:-8.17.4}

# Přidání konfiguračních souborů do nových umístění
COPY config/logstash.yml /usr/share/logstash/config/logstash.yml.custom
COPY pipeline/ /usr/share/logstash/pipeline.custom/

# Upravení entrypointu pro použití vlastních konfigurací
RUN echo '#!/bin/bash\ncp /usr/share/logstash/config/logstash.yml.custom /usr/share/logstash/config/logstash.yml\ncp -r /usr/share/logstash/pipeline.custom/* /usr/share/logstash/pipeline/\nexec /usr/local/bin/docker-entrypoint' > /usr/local/bin/custom-entrypoint.sh \
    && chmod +x /usr/local/bin/custom-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/custom-entrypoint.sh"]