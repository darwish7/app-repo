FROM python:3.7

COPY . /app

WORKDIR /app

RUN pip install -r requirements.txt

ENV ENVIRONMENT=PROD
ENV HOST=localhost
ENV PORT=8000
ENV REDIS_HOST=localhost
ENV REDIS_PORT=6379
ENV REDIS_DB=0

EXPOSE 8000

CMD ["python", "hello.py"]