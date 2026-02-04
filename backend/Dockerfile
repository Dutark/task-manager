FROM python:3.12-alpine

# Installer curl (utilisé par HEALTHCHECK)
RUN apk add --no-cache curl

# Créer un utilisateur non-root
RUN adduser -D -h /home/appuser appuser

WORKDIR /app

# Copier les dépendances d'abord (cache Docker)
COPY requirements.txt .

# Installer les dépendances
RUN pip install --no-cache-dir -r requirements.txt

# Copier le code
COPY . .

# Passer en utilisateur non-root
USER appuser

# Exposer le port
EXPOSE 8000

# Healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8000/health || exit 1

# Lancer l'API
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
