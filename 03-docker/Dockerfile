# === СТАДИЯ 1: Сборка (весит ~800 МБ) ===
FROM golang:1.20 AS builder
WORKDIR /app
# Копируем исходный код
COPY main.go .
# Компилируем программу (создаем исполняемый файл my-program)
RUN CGO_ENABLED=0 GOOS=linux go build -o my-program main.go

# === СТАДИЯ 2: Финальная (весит ~7 МБ) ===
FROM alpine:latest
WORKDIR /app
# МАГИЯ: Копируем ТОЛЬКО готовый бинарный файл из первой стадии
COPY --from=builder /app/my-program .
# Запускаем программу при старте
CMD ["./my-program"]
