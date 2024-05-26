```
FROM rust:latest

WORKDIR /usr/src/myapp
COPY . .

RUN cargo install --path .
# cargo name ex. name = "rust"
CMD ["rust"]
```

```
# build image
docker build --platform linux/amd64 -f docker/Dockerfile -t asia-northeast1-docker.pkg.dev/project_id/repository_id/rust-app:prd .

#push image to artifact registry
docker push asia-northeast1-docker.pkg.dev/project_name/repository_id/rust-app:prd
```
