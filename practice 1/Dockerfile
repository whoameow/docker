FROM python:3.11-slim

LABEL maintainer="@master"
LABEL description="kakoeto prilozhenie na flask"
LABEL version="1.0.0"

WORKDIR /app

RUN groupadd -r appuser && \
    useradd -r -g appuser -u 1001 appuser && \
    chown -R 1001:1001 /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    APP_VERSION=1.0.0 \
    ENVIRONMENT=dev \
    STUDENT_NAME=sigma

COPY requirements.txt .

RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc && \
    pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt && \
    apt-get purge -y --auto-remove gcc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY app.py .

USER appuser

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8080/health')" || exit 1

CMD ["python", "app.py"]
