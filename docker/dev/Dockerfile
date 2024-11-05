FROM python:3.9-slim

WORKDIR /app

# 開発用パッケージを含むrequirements.txtをコピー
COPY docker/dev/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ソースコードのコピー
COPY . .

# Pythonパスの設定
ENV PYTHONPATH=/app
