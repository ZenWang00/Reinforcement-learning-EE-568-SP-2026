# EE-568 Reinforcement Learning Assignment
# Python 3.10 for compatibility with numpy, scipy, torch
FROM python:3.10-slim

WORKDIR /workspace

# Install system dependencies (for matplotlib, scipy)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for better layer caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy project files
COPY . .

# Create output dirs (plot.py saves to ../plot/, ../plot/figs/)
RUN mkdir -p /plot /plot/figs /results

# Expose Jupyter port
EXPOSE 8888

# Run Jupyter Lab (use --ip=0.0.0.0 to allow external access)
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
