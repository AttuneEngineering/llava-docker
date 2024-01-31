# LLaVA Docker Images for Runpod Deployments
### LLaVA: Large Language and Vision Assistant

---

Model Link: _[here]()_
Original Container Link: _[here](https://github.com/ashleykleynhans/llava-docker)_

This repository is forked from [ashleykleynhans/llava-docker](https://github.com/ashleykleynhans/llava-docker) and reconfigured to run Flask on startup for serving an API with Runpod with a true One-Click-Template deployment.

This Docker Image is used to deploy the `LLaVA` models to Runpod provisioned GPUs using One-Click-Templates curated by Attune Engineering. For the complete list of Attune Engineering's deployment templates, check [here](https://attuneengineering.com/models.html).

---

### Available Models

> [!IMPORTANT]
> If you select a 13B or larger model, CUDA will result in OOM errors with a GPU that has less than 48GB of VRAM. At least a single A6000 or larger is recommended for 13B models

You can add an environment called MODEL to your Docker container to specify the model that should be downloaded. If the `MODEL` environment variable is not set, the model will default to liuhaotian/llava-v1.6-mistral-7b.

#### LLaVA-v1.6

| Model                                                                            | Environment Variable Value       | Version    | LLM           | Default |
|----------------------------------------------------------------------------------|----------------------------------|------------|---------------|---------|
| [llava-v1.6-vicuna-7b](https://huggingface.co/liuhaotian/llava-v1.6-vicuna-7b)   | liuhaotian/llava-v1.6-vicuna-7b  | LLaVA-1.6  | Vicuna-7B     | no      |
| [llava-v1.6-vicuna-13b](https://huggingface.co/liuhaotian/llava-v1.6-vicuna-13b) | liuhaotian/llava-v1.6-vicuna-13b | LLaVA-1.6  | Vicuna-13B    | no      |
| [llava-v1.6-mistral-7b](https://huggingface.co/liuhaotian/llava-v1.6-mistral-7b) | liuhaotian/llava-v1.6-mistral-7b | LLaVA-1.6  | Mistral-7B    | yes     |
| [llava-v1.6-34b](https://huggingface.co/liuhaotian/llava-v1.6-34b)               | liuhaotian/llava-v1.6-34b        | LLaVA-1.6  | Hermes-Yi-34B | no      |

#### LLaVA-v1.5

| Model                                                                            | Environment Variable Value       | Version   | Size | Default |
|----------------------------------------------------------------------------------|----------------------------------|-----------|------|---------|
| [llava-v1.5-7b](https://huggingface.co/liuhaotian/llava-v1.5-7b)                 | liuhaotian/llava-v1.5-7b         | LLaVA-1.5 | 7B   | no      |
| [llava-v1.5-13b](https://huggingface.co/liuhaotian/llava-v1.5-13b)               | liuhaotian/llava-v1.5-13b        | LLaVA-1.5 | 13B  | no      |
| [BakLLaVA-1](https://huggingface.co/SkunkworksAI/BakLLaVA-1)                     | SkunkworksAI/BakLLaVA-1          | LLaVA-1.5 | 7B   | no      |

---

### Building
  ```bash
  ### BUILDING
  export REGISTRY_IMAGE="ghcr.io/attuneengineering/llava-docker:v0.1"
  docker build -f Dockerfile -t $REGISTRY_IMAGE .
  
  ### PUSHING
  echo $GITHUB_TOKEN | docker login ghcr.io -u GITHUB_USERNAME --password-stdin
  docker push $REGISTRY_IMAGE

  ### PULLING
  docker pull $REGISTRY_IMAGE

  ### RUNNING
  docker run -d \
    --gpus all \
    -v /workspace \
    -p 5000:5000 \
    $REGISTRY_IMAGE
  ```

In this case, we are explicitly installing `Flask` and then running an inference server on port 5000 on start to create our endpoint.

---

## Changelog

- [01/31/2024] - Revised to match fork to match `ashleykleynhans/llava-docker` v1.3.0 and introduce LLaVA 1.6 models.
- [01/30/2024] - Published custom container image `ghcr.io/attuneengineering/llava-docker:v0.1` with Flask server deployment for Runpod inference.

---