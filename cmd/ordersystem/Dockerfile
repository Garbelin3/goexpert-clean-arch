# Etapa de build
FROM golang:1.21 AS builder
WORKDIR /app
COPY go.mod go.sum ../../
RUN go mod download
COPY . .
WORKDIR /app/cmd/ordersystem

# Etapa final
FROM golang:1.21
WORKDIR /app
COPY --from=builder /app /app
WORKDIR /app/cmd/ordersystem
EXPOSE 8080
CMD ["go", "run", "main.go", "wire_gen.go"] 