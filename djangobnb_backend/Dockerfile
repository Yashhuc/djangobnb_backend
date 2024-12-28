FROM python:3.12-slim-bullseye

WORKDIR /usr/src/djangobnb_backend

# Environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc libpq-dev netcat libjpeg-dev zlib1g-dev \
    && apt-get clean

# Upgrade pip and install setuptools, wheel
RUN pip install --upgrade pip setuptools wheel

# Copy and install dependencies
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# Handle entrypoint script
COPY ./entrypoint.sh .
RUN sed -i 's/\r$//g' /usr/src/djangobnb_backend/entrypoint.sh
RUN chmod +x /usr/src/djangobnb_backend/entrypoint.sh

# Copy project files
COPY . .

# Set entrypoint
ENTRYPOINT ["/usr/src/djangobnb_backend/entrypoint.sh"]
