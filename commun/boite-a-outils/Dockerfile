# Boite a outils DALOMIN - serie DHCP
#
# Une seule image pour tous les noeuds de toutes les topologies de la serie.
# Ce qui distingue un serveur d'un client n'est pas l'image, c'est le
# processus qu'on y lance.
#
#   docker build -t dalomin/boite-a-outils:1.0 .

FROM ubuntu:24.04

LABEL org.opencontainers.image.title="Boite a outils DALOMIN"
LABEL org.opencontainers.image.description="Noeuds Containerlab pour la serie DHCP"
LABEL org.opencontainers.image.source="https://github.com/sergesdewa/dalomin-lab"

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=America/Toronto

RUN apt-get update && apt-get install -y --no-install-recommends \
    \
    # --- clients DHCP : les comparer est le sujet des ep. 14, 16 et 34 ---
    isc-dhcp-client \
    dhcpcd-base \
    \
    # --- serveurs et relais ---
    # dnsmasq : le serveur minimal de l'ep. 3, et aussi TFTP (ep. 17) et DNS
    # kea     : le serveur de toute la serie a partir de l'ep. 4
    # d2      : les mises a jour DNS dynamiques de l'ep. 15 (RFC 4702)
    # ctrl    : l'API de controle, pour interroger les baux (ep. 35)
    # dhcrelay: l'agent relais du stade C (ep. 19 a 23)
    # isc-dhcp-server : la syntaxe d'avant Kea, pour la comparaison
    dnsmasq \
    kea-dhcp4-server \
    kea-dhcp-ddns-server \
    kea-ctrl-agent \
    kea-common \
    isc-dhcp-relay \
    isc-dhcp-server \
    \
    # --- DNS, pour les mises a jour dynamiques de l'ep. 15 ---
    bind9 \
    bind9-utils \
    dnsutils \
    \
    # --- demarrage reseau (ep. 17, RFC 4578) ---
    tftpd-hpa \
    \
    # --- capture et analyse ---
    # mergecap vient avec tshark : indispensable aux ep. 19 a 23 pour
    # fusionner les deux cotes d'un relais dans un seul fichier
    tcpdump \
    tshark \
    tcpreplay \
    \
    # --- forge de paquets : ep. 29 (serveur pirate) et 30 (epuisement) ---
    python3 \
    python3-scapy \
    \
    # --- ARP : le probe du RFC 5227, ep. 9 et 32 ---
    iputils-arping \
    \
    # --- vie privee : ep. 34, RFC 7844 ---
    macchanger \
    \
    # --- reseau de base. Pas de net-tools : on montre 'ip', pas 'ifconfig' ---
    iproute2 \
    iputils-ping \
    traceroute \
    ethtool \
    nftables \
    \
    # --- confort a l'ecran ---
    # jq : la configuration de Kea est du JSON
    jq \
    curl \
    less \
    nano \
    procps \
    ca-certificates \
    \
 && rm -rf /var/lib/apt/lists/*

# Outils dont le nom de paquet n'est pas garanti sur 24.04.
# Isoles pour qu'une absence ne fasse pas echouer la construction.
RUN apt-get update \
 && apt-get install -y --no-install-recommends udhcpc 2>/dev/null \
 || echo "udhcpc indisponible - sans consequence avant l'ep. 14" ; \
    rm -rf /var/lib/apt/lists/*

# Les services sont lances a la main dans chaque episode, jamais au demarrage.
# Le conteneur doit seulement rester en vie.
CMD ["sleep", "infinity"]
