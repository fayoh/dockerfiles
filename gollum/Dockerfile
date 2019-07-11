FROM ruby

ENV DEBIAN_FRONTEND=noninteractive
RUN     http_proxy=http://proxycluster.se.axis.com:3128 && \
	https_proxy=http://proxycluster.se.axis.com:3128 && \
	apt-get -y update && \
	apt-get -y install libicu-dev cmake && \
	rm -rf /var/lib/apt/lists/* && \
	gem install github-linguist && \
	gem install gollum && \
	unset http_proxy &&\
	unset https_proxy
COPY config.rb /etc
WORKDIR /wiki
ENTRYPOINT ["gollum", "--config", "/etc/config.rb"]
EXPOSE 80
