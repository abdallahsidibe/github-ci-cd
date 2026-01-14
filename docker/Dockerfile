# Base Node
FROM node:18-alpine

# Installer build tools et OpenSSL pour Prisma
RUN apk add --no-cache python3 make g++ openssl

# Définir le répertoire de travail
WORKDIR /usr/src/app

# Copier package.json et package-lock.json
COPY app/package*.json ./

# Installer les dépendances
RUN npm ci

# Copier tout le projet
COPY app/ .

# Générer le client Prisma
RUN npx prisma generate --schema=src/prisma/schema.prisma

# Reset Nx pour éviter les erreurs de cache dans Docker
RUN npx nx reset

# Builder le projet TypeScript / Nx
RUN npm run build

# Lancer l'application
CMD ["node", "dist/api/main.js"]
