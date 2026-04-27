FROM alpine:latest
WORKDIR /app
COPY backup .
RUN chmod +x backup
ENTRYPOINT ["./backup"]
CMD ["list"]

