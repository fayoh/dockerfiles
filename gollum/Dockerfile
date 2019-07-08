FROM ruby

ARG http_proxy
ARG https_proxy

ENV DEBIAN_FRONTEND=noninteractive
ENV http_proxy=$http_proxy https_proxy=$https_proxy
RUN apt-get -y update && apt-get -y install libicu-dev cmake && rm -rf /var/lib/apt/lists/*
RUN gem install github-linguist
RUN gem install gollum
RUN gem install org-ruby  # optional
WORKDIR /wiki
ENTRYPOINT ["gollum", "--port", "80"]
EXPOSE 80
