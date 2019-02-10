FROM ruby:2.3.3

ENV folder=app
EXPOSE 3000

#install dependencies
RUN		apt-get update -y && \
		apt-get install -y nodejs sqlite3 && \
		gem install rails

COPY $folder /opt/app
WORKDIR /opt/app

ONBUILD RUN	bundle install &&\
			rails db:migrate &&\
