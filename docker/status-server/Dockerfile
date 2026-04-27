# Stage 1: generate static html
FROM ubuntu:24.04 AS builder
WORKDIR /build
COPY generate-page .
RUN chmod +x generate-page && ./generate-page > index.html
RUN echo "Hostname: $(hostname)"

# Stage 2: production nginx (unprivileged to run as nono-root)
FROM nginxinc/nginx-unprivileged:1.28
LABEL org.opencontainers.image.source="https://github.com/user/repo"
LABEL org.opencontainers.image.version="1.0.0"
COPY --from=builder /build/index.html /usr/share/nginx/html/index.html
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
	CMD curl -f http://localhost:8080/ || exit 1

