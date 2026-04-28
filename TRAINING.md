# Retraining azoth

Reproduce an azoth build from the published sample store.

## Prerequisites

- rclone
- PostgreSQL 17+
- Go 1.25+ with CGO
- Python 3.11+
- ~200 GB free disk

## 1. Configure rclone

```bash
rclone config create r2 s3 \
  provider=Cloudflare \
  access_key_id=<your-key> \
  secret_access_key=<your-secret> \
  endpoint=https://<account-id>.r2.cloudflarestorage.com \
  region=auto

rclone lsd r2:azoth-training
```

## 2. Stand up hopper

```bash
git clone https://codeberg.org/atomdrift/hopper.git
cd hopper && make install

sudo -u postgres psql -c "CREATE ROLE hopper LOGIN PASSWORD 'changeme'; \
  CREATE DATABASE hopper OWNER hopper;"
echo 'localhost:5432:hopper:hopper:changeme' >> ~/.pgpass && chmod 600 ~/.pgpass

export DATABASE_URL='postgres://hopper@localhost:5432/hopper'
hopper init
```

## 3. Load the corpus

```bash
git clone https://codeberg.org/atomdrift/azoth-trainer.git
cd azoth-trainer
make r2-load DB="$DATABASE_URL"
hopper stats
```

## 4. Train

```bash
make train DB="$DATABASE_URL"
```

Outputs `azoth.xgb` and `azoth.onnx` under `out/`.

## 5. Evaluate

```bash
make evaluate DB="$DATABASE_URL"
```

## 6. Use it

```bash
litmus --model out/azoth.onnx suspect.bin
```
