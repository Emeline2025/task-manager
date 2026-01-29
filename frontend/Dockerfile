FROM python:3.12

RUN useradd -m appuser
USER appuser

HEALTHCHECK --interval=30s --timeout=3s --retries=3 CMD curl -f http://localhost/health || exit 1

FROM nginxinc/nginx-unprivileged:alpine3.22-perl AS nginx_src
FROM alpine:3.19
COPY --from=nginx_src /etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=nginx_src /etc/nginx/conf.d /etc/nginx/conf.d

EXPOSE 5173
CMD ["uvicorn", "app.main", "--host", "0.0.0.0", "--port", "5173"]
