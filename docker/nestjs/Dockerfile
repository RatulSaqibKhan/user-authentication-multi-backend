# Base Stage: Install Dependencies
ARG BASE_IMAGE=node
ARG IMAGE_VERSION=20.17.0
ARG IMAGE_TYPE=slim

FROM ${BASE_IMAGE}:${IMAGE_VERSION}-${IMAGE_TYPE} AS base

RUN echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list

# Set the working directory inside the container
WORKDIR /app

# Install required OS packages
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y curl iputils-ping openssl telnet \
    && rm -rf /var/lib/apt/lists/*

# Copy package.json and package-lock.json
COPY ./apps/frameworks/nestjs/package*.json ./

# Install dependencies (this includes devDependencies for now)
RUN npm install

# Copy all source files
COPY ./apps/frameworks/nestjs ./app

# Stage 1: Development
FROM base AS development

# Install development dependencies and tools
RUN npm install --only=development

# Copy SSL certificates to the container
COPY ./docker/ssl /etc/ssl

# Expose the port the app runs on
EXPOSE 3000

# Use the NestJS default for development (which includes hot-reloading)
CMD ["npm", "run", "start:dev"]

# Stage 2: Testing
FROM development AS test

# Run tests using the installed test dependencies
CMD ["npm", "run", "test"]

# Stage 3: Builder - Compile the application
FROM base AS builder

# Copy all the source files from the base stage
COPY ./apps/frameworks/nestjs/tsconfig.json /app/

# Run the build to generate the dist folder (compiling TypeScript to JavaScript)
RUN npm run build

# Stage 3: Production - Reusing from development
FROM base AS production

# Set the working directory inside the container
WORKDIR /app

# Copy only the necessary files from the builder stage
COPY --from=builder /app/dist /app/dist
COPY --from=builder /app/package*.json ./

# Install only production dependencies
RUN npm ci --omit-dev

# Copy SSL certificates (pre-generated) if required
COPY --from=development /etc/ssl /etc/ssl

# Expose the port the app runs on
EXPOSE 3000

# Start the NestJS app in production mode
CMD ["node", "dist/main"]