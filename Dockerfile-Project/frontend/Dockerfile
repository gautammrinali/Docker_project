# Stage 1: Build the application
FROM node:20-alpine AS build

WORKDIR /app

# Copy only package files first (better caching)
COPY package*.json ./

# Install dependencie
RUN npm install

# Copy rest of the code
COPY . .

# Build the app
RUN npm run build

# Stage 2: Serve using Nginx
FROM nginx:1.25-alpine

# Remove default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy build output
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]