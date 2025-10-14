# --------- Stage 1: Build the Angular app ----------
FROM node:18 AS build

# Set working directory inside container
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm ci

# Copy the rest of the application code
COPY . .

# Build the Angular app for production
RUN npm run build -- --configuration production

# --------- Stage 2: Serve with Nginx ----------
FROM nginx:alpine

# Copy built Angular files to Nginx html directory
COPY --from=build /app/dist/angular-16-crud /usr/share/nginx/html

# Expose port 80 for serving the app
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
