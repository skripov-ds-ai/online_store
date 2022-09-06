FROM golang:1.18.3-alpine AS builder
RUN apk add --update --no-cache git

COPY ./backend /online_store/backend
WORKDIR /online_store/backend

# RUN ls
RUN go mod download

RUN CGO_ENABLED=0 GOOS=linux go build -o ./.bin/app ./cmd/shop/main.go

FROM alpine:latest

RUN apk --no-cache add ca-certificates
WORKDIR /root/

COPY --from=0 /online_store/backend/.bin/app .
#COPY --from=0 /online_store/backend/pkg/config/ ./config/
#COPY --from=0 /online_store/backend/templates/ ./templates/

EXPOSE 8000

CMD [ "./app"]