# LLaVA Docker Images for Runpod Deployments

---

Forked from [ashleykleynhans/llava-docker](https://github.com/ashleykleynhans/llava-docker) and reconfigured to run Flask on startup for serving an API with Runpod with a true One-Click-Template deployment.

This Docker Image is used to deploy the `LLaVA` models to Runpod provisioned GPUs using One-Click-Templates curated by Attune Engineering.

---

### Deployment Templates
This Image is baked into the following Runpod One-Click-Template deployements:
- [BakLLaVA-1 by Attune Engineering](https://runpod.io/gsc?template=g66657xsg6&ref=zdeyr0zx)
- [LLAVA v1.5 7B by Attune Engineering](https://runpod.io/gsc?template=s44equ0gry&ref=zdeyr0zx)
- [LLAVA v1.5 13B by Attune Engineering](https://runpod.io/gsc?template=aajbtuv52q&ref=zdeyr0zx)

For the complete list of Attune Engineering's deployment templates, check [here](https://attuneengineering.com/models.html).

---

### Building
  ```bash
  ### BUILDING
  export REGISTRY_IMAGE="ghcr.io/attuneengineering/llava-docker"
  export VERSION_TAG="v0.1"
  echo $GITHUB_TOKEN | docker login ghcr.io -u GITHUB_USERNAME --password-stdin
  docker build -f Dockerfile -t $REGISTRY_IMAGE:$VERSION_TAG .
  
  ### PUSHING
  docker push $REGISTRY_IMAGE:$VERSION_TAG

  ### PULLING
  docker pull $REGISTRY_IMAGE:$VERSION_TAG

  ### RUNNING
  docker run -d \
    --gpus all \
    -v /workspace \
    -p 5000:5000 \
    ghcr.io/attuneengineering/llava-docker
  ```

---

# Custom Model Environments

### LLaVA

Adapted from the [official LLaVA Docker Image](https://github.com/ashleykleynhans/llava-docker). In this case, we are explicitly installing `Flask` and then running an inference server on port 5000 on start to create our.
  ```bash
  ghcr.io/attuneengineering/llava-docker:v0.1
  ```

---

## Changelog

- [01/31/2024] - Revised to match fork to match `ashleykleynhans/llava-docker` v1.3.0 and introduce LLaVA 1.6 models.
- [01/30/2024] - Published custom container image `ghcr.io/attuneengineering/llava-docker:v0.1` with Flask server deployment for Runpod inference.

---