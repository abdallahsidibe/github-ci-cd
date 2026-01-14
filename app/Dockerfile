FROM node:18-alpine
 
RUN apk add --no-cache openssl openssl-dev libc6-compat
 
WORKDIR /app
 
# 1. Copier les fichiers de dépendances
COPY package*.json ./
 
# 2. Installer les dépendances (y compris Nx et Prisma)
RUN npm install
 
# 3. Copier tout le code source
COPY . .
 
# 4. Générer le client Prisma (indispensable pour la base de données)
RUN npx prisma generate
 
# 5. Exposer le port
EXPOSE 3000
 
# 6. Lancer l'application via Nx
CMD ["npx", "nx", "serve", "api", "--host=0.0.0.0"]
