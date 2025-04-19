# Étape 1 : build Angular avec Tailwind
FROM node:23-alpine AS build

WORKDIR /app

# Copie package.json et lock
COPY package*.json ./

# Installation des dépendances
RUN npm install && \
 npm install tailwindcss@^3.4.0 postcss@^8.4.35 autoprefixer@^10.4.17 @tailwindcss/postcss@^4.1.4 @tailwindcss/container-queries@^0.1.1

# Copy config files
COPY angular.json .
COPY tailwind.config.js .
COPY postcss.config.js .

# Copie du code
COPY . .
ENV PUBLIC_URL=/
# Build Angular avec Tailwind CSS
RUN npm run build --configuration=production


# Étape 2 : serveur NGINX
FROM nginx:alpine@sha256:65645c7bb6a0661892a8b03b89d0743208a18dd2f3f17a54ef4b76fb8e2f2a10

# Supprimer config par défaut

# Copier les fichiers du build Angular
COPY --from=build /app/dist/frontend/browser /usr/share/nginx/html



# Copier config nginx custom (si tu en as une)

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80