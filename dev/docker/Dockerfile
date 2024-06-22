# syntax=docker/dockerfile:1
ARG GOLANG_VERSION=1.22.4
FROM golang:${GOLANG_VERSION} AS build
ARG SRC_DIR
ARG EXE_NAME

ENV GOOS=linux
ENV GOARCH=amd64
ENV CGO_ENABLED=0

WORKDIR /work
COPY ${SRC_DIR} /work

# Build service
RUN --mount=type=cache,target=/root/.cache/go-build,sharing=private \
  go build -o bin/${EXE_NAME} .

# ---
FROM scratch AS run

COPY --from=build /work/bin/${EXE_NAME} /usr/local/bin/

EXPOSE 8080
CMD ['${EXE_NAME}']