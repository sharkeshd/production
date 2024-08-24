# Stage 1: Build Stage
FROM eclipse-temurin:17-jdk AS builder

# Set the working directory
WORKDIR /app

# Copy the build files
COPY . /app

# Build the application (assuming Gradle or Maven)
# Uncomment the appropriate line depending on your build tool
# For Gradle
RUN ./gradlew build

# For Maven
# RUN mvn clean package

# Stage 2: Runtime Stage
FROM eclipse-temurin:17-jre AS runtime

# Set the working directory
WORKDIR /app

# Copy the built application from the build stage
COPY --from=builder /app/build/install/hipstershop /app

# Expose the port
EXPOSE 9555

# Set the entrypoint
ENTRYPOINT ["/app/bin/AdService"]

# Default command (optional)
CMD []
