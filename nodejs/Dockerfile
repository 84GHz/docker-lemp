# User official Node.js Docker image
FROM node:latest

#Answer 'yes' to each question
ENV DEBIAN_FRONTEND noninteractive

# Upgrade the debian packages
RUN (apt-get update && apt-get upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)

#The official image comes with npm; so we can use it to install some packages
RUN npm install -g grunt-cli gulp-cli bower grunt-sass

# Install fontforge for our specific need
RUN apt-get install -y fontforge

# Install packages and compile ttfautohint (still for our specific need)
RUN apt-get install -y libharfbuzz-dev libfreetype6-dev libqt4-dev\
    && cd /tmp \
    && curl -L http://download.savannah.gnu.org/releases/freetype/ttfautohint-1.6.tar.gz |tar xz\
    && cd ttfautohint-1.6\
    && ./configure\
    && make\
    && make install

