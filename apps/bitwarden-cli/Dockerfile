FROM node:24-alpine

WORKDIR /app

RUN apk add --no-cache bash libsecret jq curl unzip

RUN npm install -g @bitwarden/cli 
RUN mkdir -p "/home/node/.config/" && mkdir /config && ln -s /config "/home/node/.config/Bitwarden CLI"  && touch "/config/data.json" && chown -R 1000:1000 "/config"  

RUN printf '#!/usr/bin/env bash\n\
set -e\n\
\n\
rm -rf /config/*\n\
\n\
echo "Setting Bitwarden CLI server URL..."\n\
bw config server "${BW_HOST}"\n\
\n\
echo "Logging in to Bitwarden using API key..."\n\
bw login --apikey --raw\n\
\n\
echo "Unlocking Bitwarden vault using BW_PASSWORD environment variable..."\n\
export BW_SESSION=$(bw unlock --passwordenv BW_PASSWORD --raw)\n\
\n\
echo "Verifying that the Bitwarden vault is unlocked..."\n\
bw unlock --check\n\
\n\
echo "Running \`bw serve\` on port 8087..."\n\
bw serve --hostname 0.0.0.0\n' > /entrypoint.sh && chmod +x /entrypoint.sh

USER node

CMD ["/entrypoint.sh"]
