FROM tiangolo/uvicorn-gunicorn-fastapi:python3.11-slim

RUN apt update && apt upgrade -y && apt install netcat-openbsd -y

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt --no-cache-dir

COPY . .