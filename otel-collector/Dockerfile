FROM otel/opentelemetry-collector-contrib:0.69.0

ARG BRANCH

WORKDIR /source
COPY "${BRANCH}-otel-collector-config.yaml" /source/otel-collector-config.yaml

EXPOSE 4317 4318 

CMD ["--config", "/source/otel-collector-config.yaml"]