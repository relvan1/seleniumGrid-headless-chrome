FROM softcrylicqa/selenium-base

MAINTAINER Softcrylic

USER root

RUN apt-get update -qqy \
  && apt-get -qqy install \
    xvfb \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

ENV LANG_WHICH en

ENV LANG_WHERE US

ENV ENCODING UTF-8

ENV LANGUAGE ${LANG_WHICH}_${LANG_WHERE}.${ENCODING}

ENV LANG ${LANGUAGE}

RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    language-pack-en \
    tzdata \
    locales \
  && locale-gen ${LANGUAGE} \
  && dpkg-reconfigure --frontend noninteractive locales \
  && apt-get -qyy autoremove \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -qyy clean

RUN apt-get -qqy update \
  && apt-get -qqy --no-install-recommends install \
    libfontconfig \
    libfreetype6 \
    xfonts-cyrillic \
    xfonts-scalable \
    fonts-liberation \
    fonts-ipafont-gothic \
    fonts-wqy-zenhei \
    fonts-tlwg-loma-otf \
    ttf-ubuntu-font-family \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -qyy clean

USER seluser

COPY start-selenium-node.sh \
      start-xvfb.sh \
      /opt/bin/

COPY selenium.conf /etc/supervisor/conf.d/

ENV SCREEN_WIDTH 1360

ENV SCREEN_HEIGHT 1020

ENV SCREEN_DEPTH 24

ENV DISPLAY :99.0

ENV START_XVFB true

ENV NODE_MAX_INSTANCES 1

ENV NODE_MAX_SESSION 1

ENV NODE_HOST 0.0.0.0

ENV NODE_PORT 5555

ENV NODE_REGISTER_CYCLE 5000

ENV NODE_POLLING 5000

ENV NODE_UNREGISTER_IF_STILL_DOWN_AFTER 60000

ENV NODE_DOWN_POLLING_LIMIT 2

ENV NODE_APPLICATION_NAME ""

ENV GRID_DEBUG false

ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

RUN  sudo mkdir -p /tmp/.X11-unix && sudo chmod 1777 /tmp/.X11-unix
