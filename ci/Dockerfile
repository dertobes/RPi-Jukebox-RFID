FROM arm32v7/debian:buster-slim

COPY . /code
WORKDIR /code

RUN groupadd --gid 1000 pi ;\
  useradd -u 1000 -g 1000 -G sudo -d /home/pi -m -s /bin/bash -p '$1$iV7TOwOe$6ojkJQXyEA9bHd/SqNLNj0' pi ;\
  chown -R 1000:1000 /code /home/pi ;\
  chmod +x /code/scripts/installscripts/buster-install-default.sh

RUN apt-get update ;\
  apt-get -y install curl gnupg sudo ;\
  echo 'deb http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi' > /etc/apt/sources.list ;\
  echo 'deb http://archive.raspberrypi.org/debian/ buster main' > /etc/apt/sources.list.d/raspi.list ;\
  curl http://raspbian.raspberrypi.org/raspbian.public.key | apt-key add - ;\
  curl http://archive.raspberrypi.org/debian/raspberrypi.gpg.key | apt-key add - ;\
  echo 'pi ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/pi ;\
  apt-get clean ;\
  rm -rf /var/cache/apt/* /var/lib/apt/lists/*

RUN apt-get update ;\
  apt-get -y dist-upgrade --auto-remove --purge ;\
  apt-get -y install python3-pip wget build-essential git iw locales ;\
  apt-get clean ;\
  rm -rf /var/cache/apt/* /var/lib/apt/lists/*

USER pi
