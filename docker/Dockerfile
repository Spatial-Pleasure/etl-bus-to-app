FROM python:3.9-slim

WORKDIR /app

# 必要なパッケージのインストール
COPY docker/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ソースコードのコピー
COPY . .

# Pythonパスの設定
ENV PYTHONPATH=/app

# コンテナ起動時のコマンド
CMD ["python", "src/main.py"]
