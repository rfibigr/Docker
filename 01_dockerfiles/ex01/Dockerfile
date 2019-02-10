FROM debian

LABEL maintainer="Romain Fibigr <rfibigr@student.42.fr"
LABEL description="start a teamspeak server"

#port connection
EXPOSE 9987/udp
#port fichier
EXPOSE 10011
#port connexion clients
EXPOSE 30033

ENV TS3SERVER_LICENSE=accept
ENV TS_VERSION 3.6.1

#prerequis debian
RUN DEBIAN_FRONTEND=noninteractive \
	apt-get -y update && \
	apt-get -y install bzip2 wget && \
	rm -rf /var/lib/apt/lists/*

#creation d'un utilisateur pour le serveur
RUN adduser --disabled-password --gecos "" teamspeak && \
su teamspeak

#telechargement de la bonne version de teamspeak
RUN	wget https://files.teamspeak-services.com/releases/server/$TS_VERSION/teamspeak3-server_linux_amd64-$TS_VERSION.tar.bz2 && \
	tar -xf teamspeak3-server_linux_amd64-$TS_VERSION.tar.bz2 && \
	rm *.tar.bz2

WORKDIR teamspeak3-server_linux_amd64
USER teamspeak
ENTRYPOINT ["sh","ts3server_minimal_runscript.sh"]
