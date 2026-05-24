# Gebruik python image gebaseerd op Alpine Linux
FROM python:3.13.2-alpine3.21
# Werkmap in de container instellen op /app
WORKDIR '/app'
# Build-tools installeren die nodig zijn om uWSGI te compileren
RUN apk add --no-cache linux-headers g++
# Installeer flask
RUN pip install Flask
# Installeer uWSGI
RUN pip install uwsgi
# Alle lokale bestanden kopiëren naar de container
COPY ./ ./
# Maak een niet-root groep en gebruiker aan voor veiligheid
RUN addgroup -S uwsgi && adduser -S uwsgi -G uwsgi
# Wissel naar de niet-root gebruiker
USER uwsgi
# Start de app via uWSGI met de ini-config
CMD ["uwsgi", "--ini", "app.ini"]