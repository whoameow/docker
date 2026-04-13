FROM python:3.11-slim AS builder

LABEL maintainer="devops@example.com"
LABEL version="1.0.0"
LABEL description="Production app"

WORKDIR /app

COPY requirements.txt /app

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        wget \
        git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --user --no-cache-dir requests && \
    pip install flask && \
    pip install pytest && \
    pip install black

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

FROM python:3.11-slim

WORKDIR /app

RUN groupadd -r appuser && \
    useradd -r -g appuser -u 1001 appuser && \
    chown -R 1001:1001 /app

COPY --from=builder /root/.local /root/.local
COPY . .
ENV PATH=/root/.local/bin:$PATH

USER appuser

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8080/health')" || exit 1

CMD ["python", "/app/app.py"]

