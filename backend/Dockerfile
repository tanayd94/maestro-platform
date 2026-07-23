FROM python:3.12-slim

# Prevent Python from writing .pyc files
ENV PYTHONDONTWRITEBYTECODE=1

# Send logs directly to stdout/stderr
ENV PYTHONUNBUFFERED=1

# Working directory
WORKDIR /app

# Install system packages
RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    libpq-dev \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first (Docker layer caching)
COPY requirements/ requirements/

RUN pip install --upgrade pip

RUN pip install -r requirements/base.txt

# Copy project
COPY . .

# Create non-root user
RUN useradd -m django && chown -R django:django /app

USER django

# CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
CMD [ "bash" ]


# FROM python:3.12-slim

# ENV PYTHONDONTWRITEBYTECODE=1
# ENV PYTHONUNBUFFERED=1

# WORKDIR /app

# RUN apt-get update && apt-get install -y \
#     gcc \
#     libpq-dev \
#     curl \
#     && rm -rf /var/lib/apt/lists/*

# COPY requirements/ requirements/

# RUN pip install --upgrade pip

# RUN pip install -r requirements/dev.txt

# COPY . .

# RUN useradd -m django

# RUN chown -R django:django /app

# USER django

# CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]