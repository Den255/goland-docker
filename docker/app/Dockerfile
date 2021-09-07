FROM golang:1.17 as stage
WORKDIR /app
COPY ./ /app

RUN go mod download
RUN go mod verify
RUN go build -o /go-contacts

FROM gcr.io/distroless/base-debian10 as prod

WORKDIR /

COPY --from=stage /go-contacts /go-contacts

EXPOSE 8000

USER nonroot:nonroot

ENTRYPOINT ["/go-contacts"]