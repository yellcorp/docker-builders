FROM node:6-stretch

LABEL maintainer="Jim Boswell <jimb@yellcorp.org>"
LABEL version=0.0.3
LABEL description="Build image based off official Node 6.x, adding Composer \
                   (and its dependency PHP7-cli), Sass (and its dependency \
                   Ruby), and rsync"

RUN apt-get update  \
 && apt-get install -y --no-install-recommends  \
      php7.0-cli  \
      php7.0-mbstring  \
      php7.0-zip  \
      rsync  \
      ruby  \
      ruby-dev  \
 && gem update --system  \
 && gem install sass

ENV COMPOSER_ALLOW_SUPERUSER 1

# The downloaded .sig file contains only the hash. shasum wants the hash, 2 x
# space, and the path. The awk line in here makes that change and pipes it
# through to shasum

RUN curl -sSo /tmp/composer-installer.php https://getcomposer.org/installer  \
 && curl -sSo /tmp/composer-installer.sig https://composer.github.io/installer.sig  \
 && awk  \
      -v OFS="  "  \
      -v path=/tmp/composer-installer.php  \
      '{ print $1, path; }'  \
      /tmp/composer-installer.sig  \
      | shasum -a 384 -c -  \
 && php /tmp/composer-installer.php  \
      --filename composer  \
      --install-dir /usr/local/bin  \
 && rm /tmp/composer-installer.*  \
 && composer self-update

CMD [ "sh" ]
