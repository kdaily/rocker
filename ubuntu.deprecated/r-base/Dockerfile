## Emacs, make this -*- mode: sh; -*-

## start with the latest ubuntu
FROM ubuntu:latest

## This handle reaches Carl and Dirk
MAINTAINER "Carl Boettiger and Dirk Eddelbuettel" rocker-maintainers@eddelbuettel.com

## Remain current
RUN apt-get update -qq \
&& apt-get dist-upgrade -y \
&& apt-get install -y software-properties-common

## Add CRAN repo to get current R
RUN add-apt-repository "deb http://cran.rstudio.com/bin/linux/ubuntu $(lsb_release -cs)/" \
&& apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

## Update again
RUN apt-get update -qq \
&& apt-get dist-upgrade -y

## Now install R and littler, and create a link for littler in /usr/local/bin
RUN apt-get update -qq \
&& apt-get install -y --no-install-recommends \
    ed \
    less \
    littler \
    r-base \
    r-base-dev \
    r-recommended \
    vim-tiny \
    wget \
&&  ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
&&  ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
&&  install.r docopt

## Set a default CRAN Repo
RUN echo 'options("repos"="http://cran.rstudio.com", encoding="UTF-8")' >> /etc/R/Rprofile.site

## Makes a default user available via runtime flag `--user docker` 
## Note: useradd is more minimal than adduser, doesn't create home directory, etc
RUN useradd docker
## Add user to 'staff' group, granting them write privileges to /usr/local/lib
RUN addgroup docker staff
