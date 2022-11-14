
# pull the official base image
FROM python:3.8.3-alpine
# setup environment variable
ENV DockerHOME=/home/app/webapp
# set work directory
RUN mkdir -p $DockerHOME
# where your code lives
WORKDIR $DockerHOME
# copy current directory into the $DockerHome
ADD . $DockerHome
# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
# install dependencies
RUN  pip install --upgrade setuptools
COPY requirements.txt $DockerHome

RUN \
 apk add --no-cache python3 postgresql-libs && \
 apk add --no-cache --virtual .build-deps gcc python3-dev musl-dev postgresql-dev && \
 python3 -m pip install -r requirements.txt --no-cache-dir && \
 apk --purge del .build-deps

COPY . .
# run this command to install all dependencies
RUN  pip install -r requirements.txt
COPY . $DockerHome
# port where the Django app runs
EXPOSE 8000
# start server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
