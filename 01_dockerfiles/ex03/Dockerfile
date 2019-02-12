FROM debian

ENV TERM xterm
ENV	IP 192.168.99.100

EXPOSE 443 80 22

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive && apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      curl && \
	  curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash

RUN apt-get install -yq --no-install-recommends gitlab-ce

#setup HTTPS

RUN	echo "external_url \"https://192.168.99.100\"" >> /etc/gitlab/gitlab.rba && \
	echo "registry_external_url \"https://registry.example.com\"" >> /etc/gitlab/gitlab.rb && \
	echo "mattermost_external_url \"https://mattermost.example.com\"" >> /etc/gitlab/gitlab.rb

#setup SSH

CMD /opt/gitlab/embedded/bin/runsvdir-start & gitlab-ctl reconfigure && gitlab-ctl tail
