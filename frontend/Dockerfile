FROM nginx:alpine

# Installer curl pour le healthcheck
RUN apk add --no-cache curl

# Créer un utilisateur non-root
RUN adduser -D -h /home/appuser appuser

# Donner les permissions nécessaires à Nginx
RUN chown -R appuser:appuser \
    /usr/share/nginx \
    /var/cache/nginx \
    /var/run

WORKDIR /usr/share/nginx/html

# Copier les fichiers frontend
COPY . .

# Passer en utilisateur non-root
USER appuser

# Exposer le port
EXPOSE 8080

# Healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8080 || exit 1
