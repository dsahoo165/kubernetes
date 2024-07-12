# Stage 1: Build the Angular project
FROM node:16.16 AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the Angular application
RUN npm run build --prod

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Remove the default NGINX configuration file
RUN rm -rf /etc/nginx/conf.d/*

# Copy the NGINX configuration file for serving Angular applications
COPY default.conf /etc/nginx/conf.d/

# Copy the built files from the previous stage to the Nginx html directory
COPY --from=builder /app/dist/neoIntHubs /usr/share/nginx/html

# Copy the custom Nginx configuration file if you have one
# COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
