---
schema_version: "1.0.0"
document_id: "ab042be1388170ac43836686a51f9e6d99a65031042d80428261c445365c068b"
company_key: "yc-unsloth-ai"
company: "Unsloth AI"
source_id: "yc-unsloth-ai-news-import-bb4a9dd43ab2"
canonical_url: "https://unsloth.ai/blog/phi4"
published_at: "2025-01-10T00:00:00+00:00"
first_seen_at: "2026-07-24T05:34:23.482806+00:00"
fetched_at: "2026-07-28T22:01:05.353137+00:00"
content_hash: "sha256:9785fe8213300a69b9edf99830fda7f9bc3d91dabfb2262d434454ede874c838"
---

# Phi-4 Finetuning + Bug Fixes by Unsloth

# Phi-4 Finetuning + Bug Fixes by Unsloth


## Jan 10, 2025 • By Daniel & Michael


## Jan 10, 2025


## •


## By Daniel & Michael


Phi-4, Microsoft's new 14B model that performs on par with OpenAI's GPT-4o-mini is now in Unsloth!


We found & fixed 4 bugs in Phi-4, greatly increasing the model’s accuracy—details below. We previously worked with Google & Hugging Face for our[Gemma bug fixes](https://unsloth.ai/blog/gemma-bugs) and Meta with our[Llama bug fixes](https://unsloth.ai/blog/phi3) .


Unsloth makes Phi-4 finetuning 2x faster, use 70% less memory, and enables >128K context lengths which is 12x longer than Hugging Face + FA2’s 12K on a 48GB GPU.


We converted Phi-4 to Llama’s architecture for better accuracy and easier use. We also uploaded fixed Phi-4 GGUFs and[dynamic 4-bit](https://unsloth.ai/blog/dynamic-4bit) quants[here](https://huggingface.co/collections/unsloth/phi-4-all-versions-677eecf93784e61afe762afa) .


Try fine-tuning via our[Phi-4 (14B) Colab Notebook](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Phi_4-Conversational.ipynb) which fits on Google's free Tesla T4 16GB GPU.


Phi-4 Bug Fixes


## 1. Tokenizer bug fixes


The Phi-4 tokenizer interestingly uses <|endoftext|> as the BOS (beginning of sentence), EOS (end of sentence) and PAD (padding) tokens. The main issue is the EOS token is wrong - it should be <|im_end|>. Otherwise, you will get <|im_end|><|endoftext|> in generations.


## 2. Fine-tuning bug fixes


The padding token should be a designated pad token like in Llama (<|finetune_right_pad_id|>) or we can use an untrained token - for example we use <|dummy_87|>.


Using the incorrect pad token, can result in infinite generations because the pad token get masked during the loss calculations. Thus, we must use the correct pad token to not accidentally mask out the eos token, since in this case it is the same as the pad token.


## 3. Chat template issues


The Phi-4 tokenizer always adds an assistant prompt - it should only do this if prompted by add_generation_prompt. Most LLM serving libraries expect non auto assistant additions, and this might cause issues during serving.


💡 Do our fixes work?


Multiple reports from Redditors shows our fixes do in fact work! For example, using the Hugging Face[OpenLLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard#/?search=phi-4) , we see our fixes and Llama-fication of Phi-4 does better or on par with Microsoft’s official Phi-4 model!


Reddit comments show our fixes make Phi-4 inference much better:
[Exhibit #1](https://www.reddit.com/r/LocalLLaMA/comments/1hwzmqc/comment/m665h08/) : Someone’s internal multiple choice testing shows our fixed version does much better:


[Exhibit #2](https://www.reddit.com/r/LocalLLaMA/comments/1hwzmqc/comment/m65wr3e/) : Telling Phi-4 to draw an ASCII art of a house:


🦙 Llama-fication


We also ported Phi-4 directly into a Llama architecture! This allows finetuning to be much more accurate since QKV are unmerged, and gate/up are also unmerged. This allows LoRA finetuning to learn separate A matrices for each. View the uploads are[here](https://docs.unsloth.ai/get-started/all-our-models) .


🦥 Dynamic 4-bit Quants


We uploaded 4-bit bitsandbytes pre-quantized models for 4x faster downloading, however, Unsloth's[Dynamic 4-bit quant](https://unsloth.ai/blog/dynamic-4bit) shows we mustn't quantize all layers. This results in largely increased accuracy while only using 10% more VRAM.


A great example of our dynamic quants' effectiveness is through submitting our dynamic 4-bit quants to Hugging Face's OpenLLM Leaderboard. Our 4-bit dynamic quant scored nearly as high as our 16-bit version—and well above standard Bnb 4-bit and Microsoft's official 16-bit model, especially for MMLU.


We uploaded our dynamic 4-bit quants which leave some layers in 16-bit[here](https://huggingface.co/unsloth/phi-4-unsloth-bnb-4bit) .
See the activation and weight error analysis plots are below:


🛠️ Finetuning Phi-4


Phi-4 (14B)


1xL4 24GB


12x


longer context


Phi-4 (14B)


1xL4 24GB


2x


faster


Phi-4 (14B)


1xL4 24GB


>70%


less VRAM


Phi-4 finetuning fits with Unsloth in under 15GB of VRAM! It’s also 2x faster, and default uses our dynamic 4-bit quants for superior accuracy! Inference is also natively 2x faster!


Try fine-tuning Phi-4 with Unsloth in our free Google[Colab Notebook here](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Phi_4-Conversational.ipynb) . To view the rest of our notebooks and model uploads, please visit our[documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks) .


## Performance benchmarks


Model


VRAM


**🦥** Unsloth speed


**🦥** VRAM reduction


**🦥** Longer context


**🤗** Hugging Face+FA2


Phi-4


24GB


2x


70%


12x longer


1x


We tested using the Alpaca Dataset, a batch size of 2, gradient accumulation steps of 4, rank = 32, and applied QLoRA on all linear layers (q, k, v, o, gate, up, down).


💕 Thank you!


As usual, a huge thank you to everyone for using & sharing Unsloth - we really appreciate it. 🙏


As always, be sure to join our[Reddit page](https://www.reddit.com/r/unsloth/) and[Discord](https://discord.gg/unsloth) server for help or just to show your support! You can also follow us on[Twitter](https://twitter.com/unslothai) and[join our newsletter](https://unsloth.ai/newsletter/) .


Thank you for reading!


Daniel & Michael Han


🦥
10 Jan 2025
