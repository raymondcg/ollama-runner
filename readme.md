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
```

* Run Compose
```bash
podman compose up -d
```

* Shut down Containers
```bash
podman compose down # --volumes
```



### Get Models

* Identify Models you want to get from (Ollama Library)[https://ollama.com/library]
	* mistral:7b
	* llama3.1:8b
	* qwen3:8b
	* opus 4.6
* Download Models Via OpenWebUI ```Admin Panel > Settings > Models > Manage```
* Download models via command line ```ollama pull llama3.2:latest```

## OpenWeb UI

* Access OpenWebUI
```bash
localhost:3000
```

## ComfyUI

## Integrate with Visual Studio Code


