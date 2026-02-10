PLATFORMS ?= linux/amd64,linux/arm64
IMAGE_NAME ?= mem0-api-server
IMAGE_TAG ?= latest

build:
	docker build -t $(IMAGE_NAME):$(IMAGE_TAG) .

buildx_setup:
	docker buildx create --name mem0-builder --use 2>/dev/null || docker buildx use mem0-builder
	docker buildx inspect --bootstrap

buildx: buildx_setup
	docker buildx build --platform $(PLATFORMS) -t $(IMAGE_NAME):$(IMAGE_TAG) --push .

buildx_load: buildx_setup
	docker buildx build --platform $(PLATFORMS) -t $(IMAGE_NAME):$(IMAGE_TAG) --load .

run_local:
	docker run -p 8000:8000 -v $(shell pwd):/app mem0-api-server --env-file .env

.PHONY: build buildx_setup buildx buildx_load run_local
