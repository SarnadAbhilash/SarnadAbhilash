## Abhilash Sarnad

**AI Engineer — post-training, agentic systems, LLM inference, and evaluation**

AI Engineer at ETS · M.Eng. Artificial Intelligence, Duke University · San Francisco Bay Area

I build production multi-agent LLM systems, post-train models to act as agents, and work on the inference infrastructure that serves them.

### Post-training

- **[computer-use-post-training](https://github.com/SarnadAbhilash/computer-use-post-training)** — Post-trained Qwen2.5-VL-7B to operate a computer (open Jupyter, write, run, and debug code) with LoRA SFT, then one round of GRPO. On locked test sets checked by file-based verifiers, success went from 0/24 to 21/24 on the original tasks and from 13% to 70% on 35 debugging tasks. A second GRPO round did not help, so training stopped there.
- **[pixels-to-keys](https://github.com/SarnadAbhilash/pixels-to-keys)** — A Chrome Dino agent that acts from raw pixels: behavior cloning on 28k frames of my own play, then PPO with a KL penalty to the cloned policy. Full 5-minute runs on 50 held-out courses rose from 26 to 38, with all 16 changed courses improving (sign test p < 0.0001).

### Upstream contributions

- **[vLLM AIBrix](https://github.com/vllm-project/aibrix) — three merged PRs.** [#2640](https://github.com/vllm-project/aibrix/pull/2640): ModelRouter integration tests covering HTTPRoute and cross-namespace ReferenceGrant lifecycle across Deployment, ModelAdapter, RayClusterFleet, and LeaderWorkerSet workloads, plus a fix for a controller bug that deleted ReferenceGrants while non-Deployment workloads were still routing. [#2665](https://github.com/vllm-project/aibrix/pull/2665): ModelAdapter controller integration tests (Service/EndpointSlice lifecycle, readiness backoff, retry annotations) plus a controller fix so retry and scheduling annotations persist across reconcile cycles — previously the backoff state was lost on every reconcile and failing engines were retried every 10 s. [#2679](https://github.com/vllm-project/aibrix/pull/2679): wired the console's deployment detail view and Playground to live deployments and streamed chat completions.

### Inference systems

- **[ray-vllm-systems-lab](https://github.com/SarnadAbhilash/ray-vllm-systems-lab)** — One measured lifecycle from Ray Data through Ray Train/FSDP LoRA into vLLM on Ray Serve. A 48-condition, 1,920-request serving matrix on an L4: continuous batching lifted output throughput from 25.8 to 823.6 tok/s; prefix caching added +17.8% (base) and +48.4% (LoRA) long-prompt throughput at concurrency 64; agentic prompts reached 94.6% KV-block reuse for only a 6% speedup. Includes a no-GPU prefix-cache analyzer that predicts vLLM's observed hit ratio within 0.28 percentage points.
- **[inference_profiler](https://github.com/SarnadAbhilash/inference_profiler)** — A `perf`-style profiler for any OpenAI-compatible server (vLLM, SGLang, TensorRT-LLM, TGI, llama.cpp). TTFT, inter-token, and end-to-end latency percentiles; closed-loop, Poisson, and burst arrival patterns; NVML GPU sampling; queue-vs-prefill attribution; saturation-knee detection; self-contained HTML reports. Measured values and heuristic estimates are kept strictly separate.
- **[gpt2-inference-optimization](https://github.com/SarnadAbhilash/gpt2-inference-optimization)** — Profiled GPT-2 decode (GPU idle ~87% at batch 1, ~237 kernel launches per token), then wrote fused Triton GELU and LayerNorm kernels verified bit-exact against PyTorch. GELU fusion delivered +12.5% end-to-end tokens/s; the LayerNorm ablation regressed 11% and was dropped, which is documented rather than hidden.

### Evaluation and safety

- **[safety-probe](https://github.com/SarnadAbhilash/safety-probe) · [adaptive-redteam](https://github.com/SarnadAbhilash/adaptive-redteam) · [realtime-safety-monitor](https://github.com/SarnadAbhilash/realtime-safety-monitor)** — A three-layer stack: inference-time behavioral probes across decoding configurations, an adaptive prompt-mutation loop over five failure modes (sycophancy, hallucination under pressure, instruction-hierarchy failure, overconfidence, multi-turn inconsistency) with rule-based and LLM-judge scorers, and a two-stage runtime detector with per-deployment policy profiles.

### At work

At ETS I own a multi-agent assessment platform, a provider-agnostic inference layer over Bedrock, Azure OpenAI, and self-hosted vLLM, and the evaluation harnesses behind it.

**Tools I reach for:** Python, Go, PyTorch, vLLM, SGLang, Ray, Triton, Kubernetes, AWS · Claude Agent SDK, Claude Code, Codex, MCP

[LinkedIn](https://linkedin.com/in/abhilash-sarnad-5b23047a) · sarnadabhilash@gmail.com
