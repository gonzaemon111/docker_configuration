FROM ruby:2.5

ARG USER="server"
ARG UID="1000"
ARG GROUP="server"
ARG GID="1000"
ARG WORKSPACE=/home/server

ENV LANG C.UTF-8

RUN apt-get update && apt-get install -y vim less

RUN apt-get install -y build-essential libpq-dev && \
    gem install bundler

RUN mkdir -p $WORKSPACE
WORKDIR $WORKSPACE
COPY / ./
RUN bundle install 


RUN groupadd -r --gid $GID $GROUP && \
    useradd -r --uid $UID --gid $GID $USER && \
    chown -R $USER:$GROUP $WORKSPACE

USER $USER
EXPOSE  3000

