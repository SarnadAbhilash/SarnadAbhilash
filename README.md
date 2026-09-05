## Abhilash Sarnad

**AI Engineer — agentic systems, LLM inference, and evaluation**

AI Engineer at ETS · M.Eng. Artificial Intelligence, Duke University · San Francisco Bay Area

I build production multi-agent LLM systems and the inference infrastructure that serves them. Most of my work sits at the boundary between agents and serving: how agent workloads load an inference stack, how to measure that, and how to make it faster and cheaper without giving up quality.

### Upstream contributions

- **[vLLM AIBrix](https://github.com/vllm-project/aibrix) — two merged PRs.** [#2640](https://github.com/vllm-project/aibrix/pull/2640): ModelRouter integration tests covering HTTPRoute and cross-namespace ReferenceGrant lifecycle across Deployment, ModelAdapter, RayClusterFleet, and LeaderWorkerSet workloads, plus a fix for a controller bug that deleted ReferenceGrants while non-Deployment workloads were still routing. [#2665](https://github.com/vllm-project/aibrix/pull/2665): ModelAdapter controller integration tests (Service/EndpointSlice lifecycle, readiness backoff, retry annotations) plus a controller fix so retry and scheduling annotations persist across reconcile cycles — previously the backoff state was lost on every reconcile and failing engines were retried every 10 s.
- **[vLLM](https://github.com/vllm-project/vllm) — [PR #53395](https://github.com/vllm-project/vllm/pull/53395).** Documentation on measuring prefix-cache effectiveness: metric units, a hit-ratio query, controlling request order and concurrency, and why a high token hit ratio does not imply a proportional speedup.

### Inference systems

- **[ray-vllm-systems-lab](https://github.com/SarnadAbhilash/ray-vllm-systems-lab)** — One measured lifecycle from Ray Data through Ray Train/FSDP LoRA into vLLM on Ray Serve. A 48-condition, 1,920-request serving matrix on an L4: continuous batching lifted output throughput from 25.8 to 823.6 tok/s; prefix caching added +17.8% (base) and +48.4% (LoRA) long-prompt throughput at concurrency 64; agentic prompts reached 94.6% KV-block reuse for only a 6% speedup. Includes a no-GPU prefix-cache analyzer that predicts vLLM's observed hit ratio within 0.28 percentage points.
- **[inference_profiler](https://github.com/SarnadAbhilash/inference_profiler)** — A `perf`-style profiler for any OpenAI-compatible server (vLLM, SGLang, TensorRT-LLM, TGI, llama.cpp). TTFT, inter-token, and end-to-end latency percentiles; closed-loop, Poisson, and burst arrival patterns; NVML GPU sampling; queue-vs-prefill attribution; saturation-knee detection; self-contained HTML reports. Measured values and heuristic estimates are kept strictly separate.
- **[gpt2-inference-optimization](https://github.com/SarnadAbhilash/gpt2-inference-optimization)** — Profiled GPT-2 decode (GPU idle ~87% at batch 1, ~237 kernel launches per token), then wrote fused Triton GELU and LayerNorm kernels verified bit-exact against PyTorch. GELU fusion delivered +12.5% end-to-end tokens/s; the LayerNorm ablation regressed 11% and was dropped, which is documented rather than hidden.

### Evaluation and safety

- **[safety-probe](https://github.com/SarnadAbhilash/safety-probe) · [adaptive-redteam](https://github.com/SarnadAbhilash/adaptive-redteam) · [realtime-safety-monitor](https://github.com/SarnadAbhilash/realtime-safety-monitor)** — A three-layer stack: inference-time behavioral probes across decoding configurations, an adaptive prompt-mutation loop over five failure modes (sycophancy, hallucination under pressure, instruction-hierarchy failure, overconfidence, multi-turn inconsistency) with rule-based and LLM-judge scorers, and a two-stage runtime detector with per-deployment policy profiles.

### At work

At ETS I own a multi-agent assessment platform adopted across 5+ programs, a provider-agnostic inference layer over Bedrock, Azure OpenAI, and self-hosted vLLM, and the evaluation harnesses behind it: expert annotation programs, LLM-as-judge scoring against real transcripts, and a synthetic-persona platform whose 550-persona × 55-item validation study reproduced the reference psychometric benchmarks (α 0.994, QWK 0.954).

**Tools I reach for:** Python, Go, PyTorch, vLLM, SGLang, Ray, Triton, Kubernetes, AWS · Claude Agent SDK, Claude Code, Codex, MCP

[LinkedIn](https://linkedin.com/in/abhilash-sarnad-5b23047a) · sarnadabhilash@gmail.com
