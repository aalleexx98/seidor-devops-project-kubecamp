FROM golang:1.21-bullseye AS build

WORKDIR /app 

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN go build \
    -ldflags="-linkmode external -extldflags -static" \
    -tags netgo \
    -o main

FROM scratch

WORKDIR /

COPY --from=build /app/main main

CMD ["/main"]