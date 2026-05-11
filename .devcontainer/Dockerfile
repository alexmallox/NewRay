FROM debian:bookworm-slim

COPY install.sh /app/install.sh

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash git curl wget unzip tzdata openssl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN chmod +x /app/install.sh && /app/install.sh
COPY config.json /etc/config.json

RUN echo 'echo -e "\n✅ VLESS LINK:\nvless://fc9c5e39-0d52-4520-aa8b-247780369817@138.201.54.122:443?encryption=none&security=tls&sni=${CODESPACE_NAME}&fp=chrome&alpn=h3%2Ch2%2Chttp%2F1.1&insecure=0&allowInsecure=0&type=xhttp&path=%2F&mode=packet-up#github_vless"' >> /etc/bash.bashrc

CMD ["/usr/local/bin/xray", "-c", "/etc/config.json"]
