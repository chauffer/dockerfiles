FROM python:3-alpine

ENV LANG=C.UTF-8 \
     HOME=/tmp

RUN apk add --virtual=.build-deps gcc musl-dev python-dev && \
    apk add --no-cache --virtual=.run-deps bash make && \
    pip install boto3 botocore awscli aws-sam-cli && \
    apk del .build-deps
