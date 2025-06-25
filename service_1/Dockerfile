FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o main .

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/main .
EXPOSE 8001
HEALTHCHECK --interval=10s --timeout=3s CMD wget --spider -q http://localhost:8001/health || exit 1
CMD ["./main"]
