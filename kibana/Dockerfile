ARG ELASTIC_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/kibana/kibana:${ELASTIC_VERSION:-8.17.4}

# Přidání konfiguračního souboru do nového umístění
COPY config/kibana.yml /usr/share/kibana/config/kibana.yml.custom

# Upravení entrypointu pro použití vlastní konfigurace
RUN echo '#!/bin/bash\ncp /usr/share/kibana/config/kibana.yml.custom /usr/share/kibana/config/kibana.yml\nexec /usr/local/bin/kibana-docker' > /usr/local/bin/custom-entrypoint.sh \
    && chmod +x /usr/local/bin/custom-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/custom-entrypoint.sh"]