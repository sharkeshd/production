# Stage 1: Build the Go application
FROM golang:1.21 AS builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod go.sum ./

# Download the Go modules.
RUN go mod download

# Copy the source code into the container
COPY . .

# Build the Go application
RUN CGO_ENABLED=0 GOOS=linux go build -o /src/server

# Stage 2: Create the final lightweight image
FROM scratch

# Copy the Go binary from the builder stage
COPY --from=builder /src/server /src/server

# Expose port 8080
EXPOSE 8080

# Define the entrypoint
ENTRYPOINT ["/src/server"]
