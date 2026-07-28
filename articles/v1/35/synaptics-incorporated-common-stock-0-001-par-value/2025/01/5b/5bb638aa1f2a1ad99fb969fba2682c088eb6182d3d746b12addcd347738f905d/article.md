---
schema_version: "1.0.0"
document_id: "5bb638aa1f2a1ad99fb969fba2682c088eb6182d3d746b12addcd347738f905d"
company_key: "synaptics-incorporated-common-stock-0-001-par-value"
company: "Synaptics Incorporated Common Stock $0.001 Par Value"
source_id: "synaptics-incorporated-common-stock-0-001-par-value-news-import-67901354d8df"
canonical_url: "https://www.synaptics.com/company/blog/the-edge-llm-offload-story-how-synaptics-torq-enables-high-efficiency-gemma-inference"
published_at: "2025-01-31T00:00:00+00:00"
first_seen_at: "2026-07-26T02:29:20.825354+00:00"
fetched_at: "2026-07-28T21:32:04.842955+00:00"
content_hash: "sha256:6134831d8f0380eed8b3adba174de50a15d617d906a7ed1a779e83824dc91235"
---

# The Edge LLM Offload Story: How Synaptics Torq™ Enables High-Efficiency Gemma™ Inference

[Home](https://www.synaptics.com/) /[Company](https://www.synaptics.com/company/overview) /[Blog](https://www.synaptics.com/company/blog) / The Edge LLM Offload Story: How Synaptics Torq™ Enables High-Efficiency Gemma™ Inference


# The Edge LLM Offload Story: How Synaptics Torq™ Enables High-Efficiency Gemma™ Inference


May 19, 2026[Karthikeyan Shanmuga Vadivel Director, Computer Vision Architecture](https://www.synaptics.com/company/blog?author=Karthikeyan%20Shanmuga%20Vadivel) Share this article


Developers and system architects today face a growing demand to enable large language model variants on device. They are facing pressure to support transformer-capable models on constrained devices to ensure data privacy, eliminate cloud API charges, and provide offline reliability. On-device execution is also becoming a necessity to meet strict security regulations, such as Europe’s Cyber Resilience Act (CRA), while delivering the instant latency required for interactive AI assistants.


The challenge is that most Edge hardware is not designed around the dynamic execution patterns, activation bottlenecks, and memory movement demands of LLMs. Running transformer-based models with hundreds of millions of parameters on standard CPUs is significantly less efficient than running them locally on dedicated hardware. When AI workloads run on host cores—whether Arm®, RISC-V, or x86—they consume the compute capacity needed for the rest of the application stack, forcing developers to compromise on system functionality. This creates a clear need to offload these models to efficient, scalable NPU implementations.


Standard NPUs often struggle with these workloads for several reasons:


1. Transformer models like Gemma 3 270M are inherently dynamic, with sequence lengths and attention masks that grow during a conversation. Most typical Edge NPUs require static runtimes and cannot manage these shifting tensor dimensions effectively.
2. LLMs rely on expensive activation functions like GELU and Softmax that require complex iterative math, which creates latency and power consumption bottlenecks on general-purpose accelerators.
3. Memory bandwidth, rather than raw compute power, often acts as the primary bottleneck, leaving NPUs idle while they wait for massive weight matrices to arrive from memory.


Modern Edge devices demand heterogeneous Edge AI architectures that can mix and match subsystems to accelerate different aspects of inferencing. This allows for a total offload of AI acceleration to dedicated engines, freeing up the host CPU for standard application tasks. These architectures enable a graceful fallback and flexible implementation paths, moving away from one-size-fits-all solutions toward a more scalable, developer-friendly generation of hardware.


To overcome these entrenched hardware and software barriers, Synaptics and Google Research have joined forces to deliver a scalable, state-of-the-art solution for Edge intelligence. This partnership leverages a new class of Edge AI silicon designed specifically to handle the unique demands of modern transformer models. The solution is built upon three pillars.


### The Synaptics and Google Collaboration


The[Synaptics Astra™ SL2610 Product Line](https://www.synaptics.com/products/embedded-processors/sl2610-product-line) is the industry’s first line of IoT Edge AI processors that integrate the Coral NPU™ from Google Research. The Torq NPU embodies the heterogeneous philosophy by featuring both a Synaptics-developed transformer-capable core (the T1) and the Google-developed scalar RISC-V core (Coral NPU) working together to deliver efficient, on-device multimodal AI.


#### Inside Gemma 3: Architecture and Requirements


Google’s Gemma 3 270M is a compact, instruction-tuned language model. Its internal requirements include 18 transformer layers that utilize GELU activations, Softmax mechanisms, and extensive matrix multiplications. These layers create significant memory and compute bottlenecks that require specific optimization.


The compact and instruction-tuned architecture of Google’s Gemma 3 270M enables the Coralboard to serve as a high-performance, on-device conversational assistant. By offloading these transformer workloads to the Torq NPU, the system ensures the absolute data privacy and offline reliability necessary for advanced edge applications.


This local compute power facilitates tool calling from natural language, where the model functions as a smart interface to interpret user intent and trigger specific on-device functions. The platform’s ability to generate tokens in real-time also allows for offline language translation, tool calling from natural language and efficient message summarization or document processing without the costs or latency associated with cloud-based APIs.


Delivering these experiences efficiently on constrained Edge hardware, however, requires overcoming several fundamental LLM inference bottlenecks. The Torq NPU toolchain addresses these challenges through three key optimization pillars:


### Pillar 1: Static Model Conversion for Predictable Execution


Edge accelerators like the Torq NPU require static runtimes with fixed tensor dimensions, unlike dynamic cloud-based runtimes. Our compiler toolchain converts dynamic graphs into static ones to provide stability. The transformation process replaces growing KV caches with pre-allocated static tensors and implements static attention masking and position encoding. By simplifying complex training-framework graphs into standard operations, we ensure maximum hardware utilization and predictable execution timing.


### Pillar 2: Hardware-Accelerated Activation Functions


Iterative mathematical computations for GELU and Softmax consume significant energy on general-purpose hardware. Torq approximates complex activation functions by decomposing the input domain into regions processed using hardware-optimized lookup tables and linear interpolation. This avoids repeated exponentials, divisions, and other computationally expensive operations.


We achieve a 10x speedup for GELU by replacing complex math with these compact tables. For Softmax, we enable division-free attention mechanisms by decomposing operations into exponential and reciprocal table lookups. Our recent experiments show that we achieve a 12.5x inference speedup for Softmax using this LUT approach.


### Pillar 3: Mixed-Precision Weight Quantization


Memory bandwidth is the primary bottleneck for LLM inference on the Astra platform. We address this through sensitivity-guided compression, where we quantize layers based on their specific tolerance. Our strategy compresses 84% of layers to 4-bit precision while maintaining 16% of sensitive layers, such as the language modeling head, at 8-bit precision to preserve accuracy.


Using this approach, we reduce weights from 16-bit precision to only 4.3 bits on average with negligible loss in model fidelity. The system stores these weights in a compressed format and restores them to bf16 precision through on-the-fly dequantization as they stream into compute units, resulting in 2.7x higher effective throughput. We also trim vocabulary and improve runtime DMA efficiency, contributing to faster inference.


### The Combined Result: Real-World Edge AI


By combining these three pillars, the Torq NPU increases inference speed by 3.5. It also eliminates dynamic allocation overhead, achieves 10x faster activations, and provides significant memory bandwidth improvements. This delivers the full Edge advantage of local execution, including data privacy, offline reliability, instant latency, and reduced cloud costs.


Developers can explore this technology by visiting the Torq examples/demos[GitHub repository](https://github.com/synaptics-torq) to view the implementation and documentation. To begin hardware evaluation, you can[purchase](https://www.digikey.com/en/products/detail/synaptics/720-KDVSL2619-02/28960268) the Synaptics Astra SL2610 (Machina) development kit. Watch this space for the official release and upcoming availability of the new Synaptics Coralboard as we follow the latest developments from the Google I/O 2026 announcements.


#### Karthikeyan Shanmuga Vadivel


Karthikeyan is Director of AI Architecture in the Technology and Innovation group at Synaptics Incorporated, where he leads model and compiler optimization for the company’s Edge AI initiatives. Since joining Synaptics after earning his PhD from the University of California, Santa Barbara, he has advanced machine learning and biometric technologies across multiple product lines, including capacitive and optical fingerprint sensor technologies.


His work spans imaging, perception systems, and Edge AI, with a focus on training and optimizing AI models for efficient deployment on resource-constrained processors. He holds more than 20 filed patents in Edge AI model optimization, biometrics, and image and video analysis. Karthikeyan earned his PhD and Master’s degrees from UC Santa Barbara and a B.Tech. from the Indian Institute of Technology, Madras.


[Read more by Karthikeyan Shanmuga Vadivel](https://www.synaptics.com/company/blog?author=Karthikeyan%20Shanmuga%20Vadivel)


#### Sauryadeep Pal


Sauryadeep Pal is an AI Applications Engineer at Synaptics, specializing in embedded and edge AI. He has a background in computer engineering and artificial intelligence, with current work focused on adapting advanced models for deployment on embedded platforms. His expertise includes graph transformations, quantization, and pipeline design for efficient AI at the edge.


Sauryadeep holds an MS in Computer Engineering from the University of California, Irvine and a BE in Computer Engineering from Multimedia University, Malaysia.


[Read more by Sauryadeep Pal](https://www.synaptics.com/company/blog?author=Sauryadeep%20Pal)


#### Karthikeyan Shanmuga Vadivel


Karthikeyan is Director of AI Architecture in the Technology and Innovation group at Synaptics Incorporated, where he leads model and compiler optimization for the company’s Edge AI initiatives. Since joining Synaptics after earning his PhD from the University of California, Santa Barbara, he has advanced machine learning and biometric technologies across multiple product lines, including capacitive and optical fingerprint sensor technologies. His work spans imaging, perception systems, and Edge AI, with a focus on training and optimizing AI models for efficient deployment on resource-constrained processors. He holds more than 20 filed patents in Edge AI model optimization, biometrics, and image and video analysis. Karthikeyan earned his PhD and Master’s degrees from UC Santa Barbara and a B.Tech. from the Indian Institute of Technology, Madras.


[AI](https://www.synaptics.com/company/blog?category=AI)[Edge Computing](https://www.synaptics.com/company/blog?category=Edge%20Computing)
