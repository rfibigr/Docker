FROM debian

ENV TERM xterm

EXPOSE 443 80 22

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive && apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      curl && \
	  curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash

RUN apt-get install -yq --no-install-recommends gitlab-ce

#setup HTTPS
RUN	echo "letsencrypt['enable'] = false" >> /etc/gitlab/gitlab.rb && \
	openssl genrsa -out gitlab.domain.com.key 2048 && \
	openssl req -new -x509 -key gitlab.domain.com.key -out gitlab.domain.com.crt -days 3650 -subj /CN=gitlab.domain.com && \
	mkdir -p /etc/gitlab/ssl && \
	chmod 700 /etc/gitlab/ssl && \
	cp gitlab.domain.com.key gitlab.domain.com.crt /etc/gitlab/ssl && \
	echo "external_url \"https://gitlab.domain.com\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/gitlab.domain.com.crt\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/gitlab.domain.com.key\"" >> /etc/gitlab/gitlab.rb

#setup SSH
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 22" >> /etc/gitlab/gitlab.rb


CMD service ssh start && /opt/gitlab/embedded/bin/runsvdir-start & gitlab-ctl reconfigure && gitlab-ctl tail
