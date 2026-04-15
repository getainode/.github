<div align="center">

<img src="./images/ainode-logo.png" alt="AINode" width="180" />

# AINode

### Turn any NVIDIA GPU into your local AI platform.

Chat, API, and fine-tuning in your browser. One command to start.
Automatic multi-node clustering. Apache 2.0.

<br />

[![Website](https://img.shields.io/badge/ainode.dev-4A9F3A?style=for-the-badge&logo=googlechrome&logoColor=white)](https://ainode.dev)
[![Install](https://img.shields.io/badge/curl%20%7C%20bash-install%20in%2030s-4A9F3A?style=for-the-badge)](https://ainode.dev/install)
[![Docs](https://img.shields.io/badge/docs.argentos.ai-0f172a?style=for-the-badge)](https://docs.argentos.ai)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue?style=for-the-badge)](https://www.apache.org/licenses/LICENSE-2.0)

[![CUDA](https://img.shields.io/badge/CUDA-13-76B900?style=flat-square&logo=nvidia&logoColor=white)](#)
[![vLLM](https://img.shields.io/badge/vLLM-engine-ff4b4b?style=flat-square)](https://github.com/vllm-project/vllm)
[![Ray](https://img.shields.io/badge/Ray-distributed-028CF0?style=flat-square)](https://www.ray.io/)
[![Docker](https://img.shields.io/badge/container-GHCR-2496ED?style=flat-square&logo=docker&logoColor=white)](https://github.com/orgs/getainode/packages)

</div>

---

## Install in 30 seconds

```bash
curl -fsSL https://ainode.dev/install | bash
```

That's it. Pulls the unified container image, registers a systemd
service, and opens the chat UI at **http://localhost:3000**.

Distributed (multi-node) install:

```bash
AINODE_PEERS="10.0.0.2,10.0.0.3" curl -fsSL https://ainode.dev/install | bash
```

---

## What it looks like

### Distributed inference across two DGX Sparks

<img src="./images/cluster-view.png" alt="AINode cluster view — two DGX Sparks with tensor-parallel inference" width="100%" />

*Two DGX Sparks, one sharded model, 244 GB aggregated VRAM. NCCL over RoCE
at 200 Gbps on ConnectX-7.*

### Chat — streaming, OpenAI-compatible

<img src="./images/chat.png" alt="AINode chat UI" width="100%" />

### API console — LM Studio style, live request tap

<img src="./images/server-api-console.png" alt="AINode server API console" width="100%" />

### 50+ models — Hugging Face catalog, one click

<img src="./images/downloads.png" alt="AINode downloads" width="100%" />

### Fine-tune from the browser

<img src="./images/training-overview.png" alt="AINode fine-tuning dashboard" width="100%" />

### Cluster config — set TP / PP, pick the fabric, go

<img src="./images/config-cluster.png" alt="AINode cluster config" width="100%" />

---

## Projects in this org

| Repo | What it is |
|---|---|
| **[ainode](https://github.com/getainode/ainode)** | Product source — CLI, API, web UI, engines, training |
| **[ainode.dev](https://github.com/getainode/ainode.dev)** | Marketing site at [ainode.dev](https://ainode.dev) |

### Container images (public on GHCR)

```bash
docker pull ghcr.io/getainode/ainode:latest        # runtime image (~18 GB)
docker pull ghcr.io/getainode/ainode-base:latest   # eugr base + CUDA 13
```

---

## Why this exists

Most "local AI" tooling bails out the moment your model is bigger than
one GPU. The moment you need two, you're writing Ray configs, debugging
NCCL, patching vLLM, and wiring SSH bootstrap — by hand, at 2 AM.

AINode bundles that entire stack into a single container and turns
multi-node inference into a UI checkbox:

- **Auto-discovery** over UDP on your cluster subnet
- **Tensor-parallel sharding** across every GPU the cluster sees
- **Ray head + worker** formation via eugr's launcher
- **NCCL over RoCE** when ConnectX-7 + RDMA are present
- **Graceful fallback** to single-node when the cluster shrinks

If you have one GB10 or ten of them, you run the same install
command, and the thing just adds up the VRAM.

---

## Built on giants

AINode doesn't reinvent inference — it composes the best OSS runtimes
and makes them boring to operate:

- **[vLLM](https://github.com/vllm-project/vllm)** — the inference engine
- **[Ray](https://www.ray.io/)** — cross-node orchestration
- **[NCCL](https://developer.nvidia.com/nccl)** — patched for 3-node ring on GB10
- **[eugr/spark-vllm-docker](https://github.com/eugr/spark-vllm-docker)** — the blessed GB10 base image
- **[Hugging Face](https://huggingface.co/)** — model catalog

---

## Status

v0.4.0 shipped (April 2026). Distributed TP=2 verified on real GB10
hardware. See the [full state-of-play](https://github.com/getainode/ainode#state-of-distributed-inference-april-2026)
in the product README — including what works, what doesn't, and the
lessons learned getting to "it just runs."

---

<div align="center">

**Powered by [argentos.ai](https://argentos.ai)** · Apache 2.0 · Made with NVIDIA GB10

<sub>If this saved you a weekend, <a href="https://github.com/sponsors/webdevtodayjason">consider sponsoring the work</a>.</sub>

</div>
