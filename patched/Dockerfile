FROM cgr.dev/chainguard/python:latest-dev as builder

WORKDIR /app
COPY requirements.txt .
# ----->%------
USER root
RUN pip install --force-reinstall pip install git+https://github.com/fridex/pip.git@provenance-url
USER nonroot
# -----%<------
RUN pip install -r requirements.txt --user

FROM cgr.dev/chainguard/python:latest

WORKDIR /app
# Make sure you update Python version in path
COPY --from=builder /home/nonroot/.local/lib/python3.11/site-packages /home/nonroot/.local/lib/python3.11/site-packages
COPY app.py .

ENTRYPOINT ["python", "/app/app.py"]
