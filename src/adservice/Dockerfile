# Stage 1: Build stage
FROM eclipse-temurin:19 AS builder

# Set the working directory
WORKDIR /app

# Copy the build files
COPY . /app

# Install build tools if necessary (e.g., Maven, Gradle)
# For example, if you're using Gradle:
RUN apt-get update && apt-get install -y wget unzip \
    && wget https://services.gradle.org/distributions/gradle-7.6-bin.zip \
    && unzip gradle-7.6-bin.zip -d /opt \
    && ln -s /opt/gradle-7.6/bin/gradle /usr/bin/gradle

# Build the application
RUN gradle build --no-daemon

# Stage 2: Runtime stage
FROM eclipse-temurin:19

# Set the working directory
WORKDIR /app

# Copy the built application from the builder stage
COPY --from=builder /app/build/install/hipstershop /app

# Expose the port the application will run on
EXPOSE 9555

# Define the entry point for the container
ENTRYPOINT ["/app/bin/AdService"]
