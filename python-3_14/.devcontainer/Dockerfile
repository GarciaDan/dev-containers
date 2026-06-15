FROM mcr.microsoft.com/devcontainers/python:3.14

RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libssl-dev \
    libffi-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip && pip install \
    uv \
    ruff \
    mypy \
    pytest \
    pytest-cov \
    ipython \
    pre-commit
