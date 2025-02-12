# Use Node.js image to build the React app
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package files first to optimize caching
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the project files
COPY . .

# Build the React app
RUN npm run build

# Use an Nginx server to serve the built React app
FROM nginx:alpine

# Copy the build output to Nginx's default directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

