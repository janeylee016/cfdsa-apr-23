FROM python:3.8

WORKDIR /app

# copy the files
COPY requirements.txt .
COPY main.py .
COPY utils.py .
COPY run.sh .
COPY public public
COPY templates templates

RUN pip install -r requirements.txt

ENV APP_PORT=3000

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl localhost:${APP_PORT}/healthz || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT python main.py 



