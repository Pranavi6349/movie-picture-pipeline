FROM python:3.10-slim  # Changed from 3.10-alpine
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /
RUN useradd -u 1000 -m app  # Changed from adduser for Debian compatibility
RUN apt-get update && \
  apt-get install -y \
  build-essential \
  libpcre3 \
  libpcre3-dev \
  openssl \
  libffi-dev \
  && pip install pipenv

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile* /app
RUN cd /app && pipenv install --system --deploy

COPY . /app

CMD uwsgi --http :5000 --master --enable-threads -s /var/www/app/app.sock --manage-script-name --mount /=app:app
