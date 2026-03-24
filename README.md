# Docker Project 2

This repository contains **two simple web services**:

- `go-app`: a Go HTTP service on port `8080`
- `node-app`: a Node.js + TypeScript + Express service on port `3000`

Both projects expose:

- `GET /` - hello response with container/host name
- `GET /health` - health check response

## Repository Structure

```text
docker-project-2/
├── go-app/
│   ├── main.go
│   ├── Dockerfile
│   └── Dockerfile-prod
└── node-app/
    ├── src/server.ts
    ├── package.json
    ├── tsconfig.json
    └── Dockerfile
```

## Prerequisites

- Docker installed
- (Optional for local non-Docker run)
  - Go `1.21+`
  - Node.js `20+` and npm

## Project 1: Go App (`go-app`)

### Run Locally

```bash
cd go-app
go run main.go
```

Service starts on `http://localhost:8080`.

### Build and Run with Docker (single stage)

```bash
docker build -t go-app:dev -f go-app/Dockerfile go-app
docker run --rm -p 8080:8080 go-app:dev
```

### Build and Run with Docker (multi-stage production)

```bash
docker build -t go-app:prod -f go-app/Dockerfile-prod go-app
docker run --rm -p 8080:8080 go-app:prod
```

### Test Endpoints

```bash
curl http://localhost:8080/
curl http://localhost:8080/health
```

## Project 2: Node + TypeScript App (`node-app`)

### Run Locally

```bash
cd node-app
npm install
npm run build
npm start
```

Service starts on `http://localhost:3000`.

### Build and Run with Docker

```bash
docker build -t node-app:prod -f node-app/Dockerfile node-app
docker run --rm -p 3000:3000 node-app:prod
```

### Test Endpoints

```bash
curl http://localhost:3000/
curl http://localhost:3000/health
```

## Running Both Projects

Use two terminals:

1. Start the Go app (local or Docker)
2. Start the Node app (local or Docker)

Then test:

```bash
curl http://localhost:8080/health
curl http://localhost:3000/health
```
