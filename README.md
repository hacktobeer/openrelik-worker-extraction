## Openrelik worker for running image_extract on input files to extract forensic artifacts

### Installation
Add the below configuration to the OpenRelik `docker-compose.yml` file.

```
testopenrelik-worker-extraction:
    container_name: openrelik-worker-extraction
    image: ghcr.io/openrelik/openrelik-worker-extraction:${OPENRELIK_WORKER_ARTIFACT_EXTRACTION_VERSION:-latest}
    restart: always
    environment:
      - REDIS_URL=redis://openrelik-redis:6379
      - OPENRELIK_PYDEBUG=0
    volumes:
      - ./data:/usr/share/openrelik/data
    command: "celery --app=src.app worker --task-events --concurrency=4 --loglevel=INFO -Q openrelik-worker-extraction"
```
