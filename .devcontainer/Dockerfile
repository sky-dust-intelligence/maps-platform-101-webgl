# Use the official Node.js image as the base
FROM node:18.16
# Install any additional OS packages you need for geo-maps
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    build-essential \
    libgeos-dev \
    gdal-bin \
    proj-bin \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install project dependencies
RUN npm ci

# Expose the app's port
EXPOSE 3000

# Set the container to use a non-root user
RUN useradd --create-home --shell /bin/bash nodeuser
USER nodeuser

# Start the app
CMD ["npm", "start"]
