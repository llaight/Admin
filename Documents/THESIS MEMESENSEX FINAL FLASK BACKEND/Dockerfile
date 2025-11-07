# Use official Python image
FROM python:3.11-slim

# Create a non-root user
RUN useradd -m -u 1000 user
USER user
ENV PATH="/home/user/.local/bin:$PATH"

# Set working directory
WORKDIR /home/user/app

# Copy backend files
COPY --chown=user . .

# Copy pre-built React frontend
COPY --chown=user frontend/memesensex-frontend/build frontend_build

# Install Python dependencies
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# Set Flask environment variables
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
ENV FLASK_RUN_PORT=7860
ENV FLASK_STATIC_FOLDER=/home/user/app/frontend_build

# Expose port
EXPOSE 7860

# Start the Flask app
CMD ["gunicorn", "-w", "1", "-b", "0.0.0.0:7860", "app:app"]