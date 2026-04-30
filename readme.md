# Local AI Runner #
* Author: Raymond Gillett
* Level: Basic
* Technologies: 
* Summary: This project is used to 
* Target Product / Container: Currently running as docker containers.

## TODO
* [x] Instructions on downloading models in Ollama
* [ ] Make sure that Ollama uses the right GPU - Seems to be using the CPU right now
* [ ] Run Comfyui in Podman -- (Docker Hub Example)[https://hub.docker.com/r/yanwk/comfyui-boot]
* [ ] Setup Visual Studio Code
* [ ] Claude Code
* [ ] Chat GPT

## Run via Podman

* Enable nvidia container toolkit in Podman Machinee
```bash
podman machine ssh
# curl -s -L https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo | \
   sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo
# sudo yum install -y nvidia-container-toolkit
# sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
# nvidia-ctk cdi list
```

* If successful, ```nvidia-ctk cdi list``` will show all the devices.

* Create/Update .env configuration file in root of this project

```
ComfyUI_Folder=
ComfyUI_Models=
ComfyUI_Port=8000
Ollama_Folder=
Openwebui_Port=3000
VLLM_MODEL=facebook/opt-125m # Replace 'facebook/opt-125m' with your desired model
```

* Create folder structure on host for volumes mapped to Comfyui.

* Run Compose
```bash
podman compose up -d
```

* Shut down Containers
```bash
podman compose down # --volumes
```

### Common Error

* Occasionally you get errors and have to regenerate the CDI in ```podman machine ssh```
```bash
nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml && \
nvidia-ctk cdi list
~~~

### Get Models

* Identify Models you want to get from (Ollama Library)[https://ollama.com/library]
	* mistral:7b - Max Context 32,768
	* llama3.2:1b - Max Context 128,000
	* llama4:16x17b - model requires more system memory (43.9 GiB) than is available (16.6 GiB)
	* qwen3.5:0.8b - Max Context 262,144
	* qwen3.5:9b - Max Context 262,144
	* qwen3.5:35b - Max Context 262,144
	* qwen3-coder-next:latest - Max Context 262,144 - model requires more system memory (22.4 GiB) than is available (16.3 GiB)
* Download Models Via OpenWebUI ```Admin Panel > Settings > Models > Manage```
* Download models via command line ```ollama pull llama3.2:latest```

## OpenWeb UI

* Access OpenWebUI
```bash
localhost:3000
```

## ComfyUI

## Integrate with Visual Studio Code


## Ollama configuration

* Max context size (Ollama defaults to 2k tokens)
```bash
/set parameter num_ctx 32768
/save qwen2.5max
```

* Start with Q4 model with flash attention, and test use case. If smooth go to Q2 or Q3, if problems go to Q8 or more.