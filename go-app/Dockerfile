#? old way

# FROM golang:1.21
# WORKDIR /app 
# COPY main.go .
# RUN go build -o server main.go
# CMD [ "./server" ]

#? New way 

# Build stage
FROM golang:1.21 AS builder
WORKDIR /app 
COPY main.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -o server main.go

# Runtime stage
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/server .
CMD [ "./server" ]