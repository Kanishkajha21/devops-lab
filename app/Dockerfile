# Base image
FROM python:3.12-slim

# Working directory
WORKDIR /app

# Copy requirements first
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code
COPY . .

# Environment variables
ENV FLASK_ENV=production
ENV REDIS_HOST=redis

# Expose port
EXPOSE 5000

# Health check
HEALTHCHECK --interval=30s --timeout=5s \
  CMD curl -f http://localhost:5000/health || exit 1

# Run app
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "2", "app:app"]
