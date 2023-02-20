FROM python:3.7-slim-buster

ADD . /app
WORKDIR /app

RUN pip install mlflow==1.22.0\
                pymysql\
                pysftp
                # google-cloud-storage\

COPY wait-for-it.sh wait-for-it.sh
RUN chmod +x wait-for-it.sh