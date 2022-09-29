FROM golang:1.19-alpine AS builder
WORKDIR /app
COPY go.mod .
RUN go mod download
COPY main.go .
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM scratch
WORKDIR /app
COPY --from=builder /app/main .

EXPOSE 8080
CMD ["./main"]
