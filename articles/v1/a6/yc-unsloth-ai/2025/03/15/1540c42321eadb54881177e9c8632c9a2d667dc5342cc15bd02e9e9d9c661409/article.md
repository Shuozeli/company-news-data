---
schema_version: "1.0.0"
document_id: "1540c42321eadb54881177e9c8632c9a2d667dc5342cc15bd02e9e9d9c661409"
company_key: "yc-unsloth-ai"
company: "Unsloth AI"
source_id: "yc-unsloth-ai-news-import-bb4a9dd43ab2"
canonical_url: "https://unsloth.ai/blog/gemma3"
published_at: "2025-03-14T00:00:00+00:00"
first_seen_at: "2026-07-24T05:34:23.482806+00:00"
fetched_at: "2026-07-28T21:30:42.971376+00:00"
content_hash: "sha256:691f6ff29804a19beb757990aae7e2c9c91180af9eeaadc8340dff5d09417a5e"
---

# Fine-tune & Run Gemma 3

# Fine-tune & Run Gemma 3


## Mar 14, 2025 • By Daniel & Michael


## Mar 14, 2025


## •


## By Daniel & Michael


Gemma 3, Google's new SOTA multimodal (text + image) models come in 1B, 4B, 12B, and 27B sizes including a new 270M size. Now supported in Unsloth, Gemma 3 has a 128K context window, and multilingual support.


***Update August 14:*** Gemma's new 270M model -[Run](https://huggingface.co/collections/unsloth/gemma-3-67d12b7e8816ec6efa7e4e5b) &[fine-tune](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Gemma3_(270M).ipynb) it!
***Update March 19:*** Read about our new Gemma 3[training fixes here](https://unsloth.ai/blog/gemma3#fixes)


- Fine-tune Gemma 3 for free using our[Colab notebook](https://docs.unsloth.ai/get-started/unsloth-notebooks) . Also, view our Gemma 3 (1B)[GRPO notebook](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/HuggingFace%20Course-Gemma3_(1B)-GRPO.ipynb)
- Unsloth makes Gemma 3 finetuning 1.6x faster, use 60% less VRAM, and enables 6x longer than environments with Flash Attention 2 on a 48GB GPU.
- We uploaded all versions of Gemma 3, including 2-8 bit GGUFs, dynamic 4-bit, and 16-bit versions, on[Hugging Face here](https://huggingface.co/collections/unsloth/gemma-3-67d12b7e8816ec6efa7e4e5b) . Also fixed an issue where previously our GGUFs did not have vision support.


- Read our guide on How to correctly[Run Gemma 3 here](https://docs.unsloth.ai/basics/tutorial-how-to-run-gemma-3-effectively) .


Unsloth now also supports[EVERYTHING](https://unsloth.ai/blog/gemma3#everything) * including: full fine-tuning, 8-bit, pretraining, ALL transformer-style models (Mixtral, MOE, Cohere etc.) and ANY training algorithms like GRPO with VLMs. Multi-GPU is also coming in the next few weeks - so join our[newsletter](https://unsloth.ai/newsletter) to be notified when it launches!


Big thanks to the Gemma team for collabing with us and featuring Unsloth in their[Gemma 3 Blogpost](https://developers.googleblog.com/en/introducing-gemma3/) .


Get the latest stable Unsloth via:


` pip install --upgrade --force-reinstall --no-cache-dir unsloth unsloth_zoo` ✨Gemma 3 Training Fixes


First, before we finetune or run Gemma 3, we found that when using float16 mixed precision, gradients and activations become infinity unfortunately. This happens in T4 GPUs, RTX 20x series and V100 GPUs where they only have float16 tensor cores.


Our solution in Unsloth is 3 fold:


- Keep all intermediate activations in bfloat16 format - can be float32, but this uses 2x more VRAM or RAM (via Unsloth's async gradient checkpointing)
- Do all matrix multiplies in float16 with tensor cores, but manually upcasting / downcasting without the help of Pytorch's mixed precision autocast.
- Upcast all other options that don't need matrix multiplies (layernorms) to float32.


This means **Unsloth is the only framework which works in float16 machines for Gemma 3** ! This also means Colab Notebooks with free Tesla T4 GPUs also work!


Gemma 3 (27B) finetuning fits with Unsloth in under 22GB of VRAM! It’s also 1.6x faster, and default uses Unsloth[dynamic 4-bit](https://unsloth.ai/blog/gemma3#dynamic) quants for superior accuracy! You can also use Gemma 3 directly with Unsloth's GRPO to train your own reasoning model.


Try fine-tuning Gemma 3 (4B) with Unsloth in our free Google[Colab Notebook here](https://docs.unsloth.ai/get-started/unsloth-notebooks) . To view all our notebooks and model uploads, please visit our[documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks) .


We also collaborated with Hugging Face on a[R1 Reasoning course](https://huggingface.co/learn/nlp-course/en/chapter12/6) !


✨Gemma 3 Quirks - Infinite Activation


Graph below: Gemma 3 1B to 27B exceed float16's maximum of 65504


For newer GPUs like RTX 30x or higher, A100s, H100s etc, these GPUs have bfloat16 tensor cores, so this problem does not happen! But why?


Float16 can only represent numbers up to 65504, whilst bfloat16 can represent huge numbers up to 10^38! But notice both number formats use only 16bits! This is because float16 allocates more bits so it can represent smaller decimals better, whilst bfloat16 cannot represent fractions well.


But why float16? Let's just use float32! But unfortunately float32 in GPUs is very slow for matrix multiplications - sometimes 4 to 10x slower! So we cannot do this.


## Performance benchmarks


Model


VRAM


**🦥** Unsloth speed


**🦥** VRAM reduction


**🦥** Longer context


**🤗** Hugging Face+FA2


Gemma-3-12B


24GB


1.7x


>60%


6xlonger


1x


We tested using the Alpaca Dataset, a batch size of 2, gradient accumulation steps of 4, rank = 32, and applied QLoRA on all linear layers (q, k, v, o, gate, up, down).


🦥 Everything support + Updates


Preliminary support for full-finetuning and 8-bit finetuning - set full_finetuning = True and load_in_8bit = True respectively. Both will be optimized further in the future! A reminder you will need more powerful GPUs!


New Unsloth Auto Model support - nearly all models are now supported! Unsloth now supports vision and text models out of the box, without the need for custom implementations (and all are optimized). This allows for a faster and less error prone + more stable/streamlined finetuning experience.


We also support: Qwen's[QwQ-32B](https://unsloth.ai/blog/qwq-32b) , Mistral's[Mixtral](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1) , IBM's[3.2 Granite](https://huggingface.co/unsloth?search_models=granite) , Microsoft's[Phi-4-mini](https://huggingface.co/collections/unsloth/phi-4-all-versions-677eecf93784e61afe762afa) , Cohere's[c4ai-command-a](https://huggingface.co/unsloth/c4ai-command-a-03-2025-unsloth-bnb-4bit) , AllenAI's[OLMo-2](https://huggingface.co/unsloth?search_models=olmo) and every other transformer-style model out there! We also uploaded dynamic 4-bt and GGUFs for these models.


Many multiple optimizations in Unsloth allowing a further +10% less VRAM usage, and >10% speedup boost for 4-bit (on top of our original 2x faster, 70% less memory usage). 8-bit and full finetuning also benefit.


[Windows support](https://docs.unsloth.ai/get-started/installing-+-updating/windows-installation) via pip install unsloth should function now! Utilizes 'pip install[triton-windows](https://pypi.org/project/triton-windows/) ' which provides a pip installable path for Triton.


Conversions to llama.cpp GGUFs for 16bit and 8bit now DO NOT need compiling! This solves many many issues, and this means no need to install GCC, Microsoft Visual Studio etc.


[Vision fine-tuning](https://unsloth.ai/blog/vision) : Train on completions / responses only for vision models supported! Pixtral and Llava finetuning are now fixed! In fact nearly all vision models are supported out of the box! Vision models now auto resize images which stops OOMs and also allows truncating sequence lengths.


GRPO in Unsloth now allows non Unsloth uploaded models to be in 4bit as well - reduces VRAM usage a lot! (ie using your own finetune of Llama)


New training logs and infos - training parameter counts, total batch size


Complete[gradient accumulation bug fix](https://unsloth.ai/blog/long-context) coverage for all models!


🔮 Gemma 3 Analysis


Here's an in depth analysis we did for Gemma 3's architecture:
1. 1B text only, 4, 12, 27B Vision + text. 14T tokens
2. 128K context length further trained from 32K
3. Removed attn softcapping. Replaced with QK norm
4. 5 sliding + 1 global attn
5. 1024 sliding window attention
6. RL - BOND, WARM, WARP


## Detailed Analysis


1. Architectural differences to Gemma 2:
More sliding windows are added to reduce KV cache load! A 5:1 ratio was found to work well, and ablations show 7:1 even work ok! SWA is 1024 - ablations show 1024 to 2048 work well.


2. Training, post-training
Gemma-3 uses TPUs, and Zero-3 like algos with JAX. 27B was trained on 14 trillion tokens. 12B = 12T, 4B = 4T and 1B = 2T tokens. All used distillation in the RL / post-training stage. Sampled 256 logits per token from a larger instruct model (unsure which - maybe a closed source one?). Used RL algos like BOND, WARM and WARP.


3. Chat template now forces a BOS token! Uses <start_of_turn>user and <start_of_turn>model. 262K vocab size. SentencePiece tokenizer with split digits, preserved whitespace & byte fallback.


4. Long Context & Vision Encoder:
Trained from 32K context, then extended to 128K context. RoPE Scaling of 8 was used. Pan & Scan algo was used for vision encoder. Vision encoder operates at a fixed resolution of 896 * 896. Uses windowing during inference time to allow other sizes.


🦥 Dynamic BnB 4-bit Quants


We uploaded Unsloth[Dynamic 4-bit](https://unsloth.ai/blog/dynamic-4bit) quants for Gemma 3, delivering a significant accuracy boost over standard 4-bit - especially for vision models, where the difference is most pronounced. As shown in our previous[Qwen2-VL experiments](https://unsloth.ai/blog/dynamic-4bit#QwenVL) , our dynamic quants provided substantial accuracy gains with only a 10% increase in VRAM usage.


A great benchmark example is our dynamic 4-bit quant for Phi-4, submitted to Hugging Face's OpenLLM Leaderboard. It scored nearly as high as our 16-bit version—and outperformed both standard BnB 4-bit and Microsoft’s official 16-bit model, particularly on MMLU.


Also see the activation and weight error analysis plots for Gemma 3 (27B) compared to Unsloth Dynamic quants further below:


💕 Thank you!


A huge thank you to the Google team for their support and everyone for using & sharing Unsloth - we really appreciate it. 🙏


As always, be sure to join our[Reddit page](https://www.reddit.com/r/unsloth/) and[Discord](https://discord.gg/unsloth) server for help or just to show your support! You can also follow us on[Twitter](https://twitter.com/unslothai) and[join our newsletter](https://unsloth.ai/newsletter/) .


Thank you for reading!


Daniel & Michael Han


🦥
14 Mar 2025
