FROM python:3.6-alpine3.9

WORKDIR /flask

COPY hits/app.py .
COPY requirements.txt .


RUN apk update && pip install -r requirements.txt && mkdir logs

EXPOSE 5000

ENTRYPOINT ["python"]

CMD ["app.py"]

