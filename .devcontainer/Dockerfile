FROM debian:bookworm-slim

COPY install.sh /app/install.sh

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash git curl wget unzip tzdata openssl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN chmod +x /app/install.sh && /app/install.sh
COPY config.json /etc/config.json

RUN echo '\
ips=("94.130.33.41" "94.130.13.19" "138.201.54.122" "138.201.54.122" \
"94.130.33.41" "85.10.207.48" "94.130.13.19" "65.109.34.234" \
"94.130.50.12" "65.109.34.234" "95.216.69.37" "94.130.50.12"  \
"50.7.5.83" "85.10.207.48" "50.7.5.83" "95.216.69.37" \
"50.7.87.5" "50.7.87.3" "50.7.87.4" "50.7.87.4" \
"50.7.87.2" "50.7.87.5" "50.7.87.2" "50.7.87.3" \
"63.141.252.203" "204.12.196.34" "63.141.252.203" "204.12.196.34" \
); \
echo -e "\n🚀 VLESS LINKS:\n"; \
for ip in "${ips[@]}"; do \
    echo -e "vless://fc9c5e39-0d52-4520-aa8b-247780369817@${ip}:443?encryption=none&security=tls&sni=${CODESPACE_NAME}-443.app.github.dev&fp=chrome&alpn=h3%2Ch2%2Chttp%2F1.1&insecure=0&allowInsecure=0&type=xhttp&path=%2F&mode=packet-up#github_vless\n"; \
done' >> /etc/bash.bashrc

CMD ["/usr/local/bin/xray", "-c", "/etc/config.json"]
