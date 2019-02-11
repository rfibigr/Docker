FROM ubuntu:16.04

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      curl

RUN curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install gitlab-ce && \






#add url to gitlab.rb
edit /etc/gitlab/gitlab.rb:
external_url "https://gitlab.example.com"

###create ssl key
#create ssl directory
mkdir -p /etc/gitlab/ssl
sudo chmod 700 /etc/gitlab/ssl
#create ssl certificates

#copy key in folder
cp gitlab.example.com.key gitlab.example.com.crt /etc/gitlab/ssl/



#configure firewall
