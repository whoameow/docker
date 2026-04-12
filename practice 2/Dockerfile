FROM cr.yandex/mirror/python:3.11-slim

WORKDIR /app

ENV REGISTRY="Yandex Mirror"

ENV PYTHONUNBUFFERED=1

COPY app.py .

RUN groupadd -r appuser && \
    useradd -r -g appuser -u 1001 appuser && \
    chown -R 1001:1001 /app
USER appuser

EXPOSE 8080

CMD ["python", "-u", "app.py"]
