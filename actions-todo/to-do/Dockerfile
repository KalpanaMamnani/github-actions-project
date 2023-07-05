# Stage 1: Build the React app
FROM node:14-alpine as build

WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app's source code to container
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the built app with Nginx
FROM nginx:alpine

# Remove default Nginx configurations
RUN rm -rf /etc/nginx/conf.d

# Copy Nginx configurations
COPY conf /etc/nginx

# Copy the built React app from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 for the Nginx server
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
