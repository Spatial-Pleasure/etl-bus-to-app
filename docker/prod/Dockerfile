FROM python:3.9-slim

WORKDIR /app

# 本番用の最小限のrequirements.txtをコピー
COPY docker/prod/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ソースコードのコピー
COPY . .

# Pythonパスの設定
ENV PYTHONPATH=/app
