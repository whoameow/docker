FROM python:3.11-slim

WORKDIR /app

ENV APP_NAME="Backend"

COPY app.py .

RUN chown -R 1001:1001 /app
USER 1001

CMD ["python", "app.py"]