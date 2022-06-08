FROM ruby:3.0.4

ENV RAILS_ROOT /project


RUN curl https://deb.nodesource.com/setup_12.x | bash
RUN curl https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list


RUN apt-get update && \
  apt-get install -y \
  build-essential \
  nodejs \
  yarn \
  libpq-dev && \
  mkdir -p $RAILS_ROOT && \
  apt-get clean autoclean && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log

WORKDIR $RAILS_ROOT

ENV RAILS_ENV='development'

COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
RUN gem install bundler 
RUN bundle install --without production test

COPY package.json package.json
COPY yarn.lock yarn.lock


COPY . .


