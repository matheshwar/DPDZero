FROM python:3.13-slim
WORKDIR /app
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /usr/local/bin/
COPY pyproject.toml uv.lock ./
RUN uv sync --frozen --no-cache
COPY app.py ./
EXPOSE 8002
CMD ["uv", "run", "python", "app.py"]