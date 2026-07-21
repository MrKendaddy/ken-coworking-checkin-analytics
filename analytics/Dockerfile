# Use a lightweight, current Python base image (avoids EOL Debian mirror issues)
FROM python:3.10-slim

# Set the working directory inside the container

WORKDIR /app

# Copy only requirements first so Docker can cache this layer separately
# from application code changes, speeding up rebuilds

COPY requirements.txt .

# Install Python dependencies (includes psycopg2-binary, which ships its own
# compiled Postgres client libs, so no extra system packages are needed)

RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code into the container

COPY . .

# Document the port the Flask app listens on (see APP_PORT in app.py)
EXPOSE 5153

# Run the app using exec form so it receives OS signals (e.g. SIGTERM)
# directly, allowing graceful shutdown instead of an intermediate shell
CMD ["python", "app.py"]
