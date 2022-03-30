# pull official base image for system
FROM python:3.10.1-slim-buster as builder

# set working directory
WORKDIR /usr/src

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update \
  && apt-get -y --no-install-recommends install netcat gcc \
  && apt-get clean

# copy project files
COPY ./pyproject.toml .
COPY ./setup.cfg .

# install python dependencies and make monkeypatch for poetry build-backend
RUN mkdir app \
  && touch ./app/fastapi-template.py \
  && touch ./app/__init__.py

# install app dependencies
RUN pip install --upgrade pip
RUN pip install /usr/src

# add app
COPY ./app ./app
