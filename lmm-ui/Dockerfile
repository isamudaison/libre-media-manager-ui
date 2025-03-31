# Stage 1: Build the React app
FROM node:16-alpine AS build
WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the app and build
COPY . ./
RUN npm run build

# Stage 2: Serve the app using Nginx
FROM nginx:alpine
# Remove the default Nginx static assets
RUN rm -rf /usr/share/nginx/html/*
# Copy the build folder from the previous stage
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
