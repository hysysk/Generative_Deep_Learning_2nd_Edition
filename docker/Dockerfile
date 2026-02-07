FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# h5pyビルドに必要なもの + 既存依存
RUN apt-get update && apt-get install -y --no-install-recommends \
  unzip graphviz curl musescore3 \
  python3-pip python3-dev \
  build-essential pkg-config \
  libhdf5-dev \
  && rm -rf /var/lib/apt/lists/*

# pip周り強化
RUN python3 -m pip install --upgrade pip setuptools wheel

# h5pyがnumpyヘッダを必要とすることがあるので先に入れておく（特にビルドに落ちたとき）
# ※ numpy 2.x は古い依存と衝突しやすいので <2 に抑える
RUN python3 -m pip install --upgrade "numpy<2" cython

WORKDIR /app

COPY ./requirements.txt /app/requirements.txt
RUN python3 -m pip install -r /app/requirements.txt

# Hack to get around tensorflow-io issue - https://github.com/tensorflow/io/issues/1755
RUN python3 -m pip install tensorflow-io \
  && python3 -m pip uninstall -y tensorflow-io

# パス修正（先頭 / を削除）
COPY ./notebooks/ /app/notebooks
COPY ./scripts/ /app/scripts

ENV PYTHONPATH="${PYTHONPATH}:/app"
