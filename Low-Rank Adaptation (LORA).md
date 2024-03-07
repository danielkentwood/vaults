# Low-Rank Adaptation (LORA)

##### Metadata
created:: 2023-05-10 17:04
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: 
***
From Perplexity.ai:

Low-Rank Adaptation (LoRA) is a training method that accelerates the training of large language models while consuming less memory [1](https://huggingface.co/docs/diffusers/main/en/training/lora). It works by freezing the pre-trained model weights and injecting trainable rank decomposition matrices (called update matrices) into each layer of the Transformer architecture [2](https://arxiv.org/abs/2106.09685)[3](https://openreview.net/forum?id=nZeVKeeFYf9). This greatly reduces the number of trainable parameters for downstream tasks, making the adaptation process more efficient and cost-effective [4](https://devinschumacher.hashnode.dev/lora-low-rank-adaptation-of-large-language-models). LoRA has several advantages, including:

- Preserving pretrained weights, reducing the risk of catastrophic forgetting [1](https://huggingface.co/docs/diffusers/main/en/training/lora)
- Significantly fewer parameters than the original model, making trained LoRA weights easily portable [1](https://huggingface.co/docs/diffusers/main/en/training/lora)
- On-par or better performance compared to fine-tuning in model quality on various models, despite having fewer trainable parameters, higher training throughput, and no additional inference latency [3](https://openreview.net/forum?id=nZeVKeeFYf9)

LoRA matrices are generally added to the attention layers of the original model [1](https://huggingface.co/docs/diffusers/main/en/training/lora).


## External Resources