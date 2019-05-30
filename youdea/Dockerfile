# Use an official Python runtime as a parent image
FROM python:3.7-alpine
LABEL maintainer="Brian Nyamu <brianbryo@gmail.com>"

WORKDIR /code/

# install psycopg2
RUN apk update \
    && apk add --virtual build-deps gcc python3-dev musl-dev \
    && apk add build-base jpeg-dev zlib-dev \
    && apk add postgresql-dev \
    && pip install psycopg2 \
    && apk del build-deps

# Set environment varibles
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

COPY ./requirements.txt /code/requirements.txt
RUN pip install --upgrade pip
# Install any needed packages specified in requirements.txt
RUN pip install -r /code/requirements.txt
RUN pip install gunicorn

# Copy the current directory contents into the container at /code/
COPY . /code/
# Set the working directory to /code/

#USER wagtail

EXPOSE 8000
#CMD exec gunicorn youdea.wsgi:application --bind 0.0.0.0:8000 --workers 3

# run entrypoint.prod.sh
CMD ["./code/entrypoint.prod.sh"]
