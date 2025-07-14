FROM node:24-alpine

WORKDIR /app

RUN apk add --no-cache bash libsecret jq curl unzip

RUN npm install -g @bitwarden/cli 
RUN mkdir -p "/home/node/.config/" && mkdir /config && ln -s /config "/home/node/.config/Bitwarden CLI"  && touch "/config/data.json" && chown -R 1000:1000 "/config"  

RUN printf '#!/usr/bin/env bash\nset -e\n\nbw config server "${BW_HOST}"\nbw login --apikey --raw\nexport BW_SESSION=$(bw unlock --passwordenv BW_PASSWORD --raw)\n\nbw unlock --check\n\necho '\''Running `bw serve` on port 8087'\''\nbw serve --hostname 0.0.0.0\n' > /entrypoint.sh && chmod +x /entrypoint.sh

USER node

CMD ["/entrypoint.sh"]
