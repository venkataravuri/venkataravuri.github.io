---
title: ML Model Compression - A practicle guide to Pruning, Quantization and Distillation
description: Reduce size of ML models without loosing their performance and efficiency and improving inferences speed usng techniques such as Pruning, Quantization and Distillation.
slug: model-compression
date: 2024-02-21 00:00:00+0000
image: cover.jpg
tags:
    - PyTorch
weight: 1 # You can add weight to some posts to override the default sorting (date descending)
---

Deep learning models often have too many parameters, which require significant GPU resources and time for inference. Model compression techniques makes models smaller and simpler without losing their effectiveness by reducing number of parameters. Compression benefits,
1. Reduce the size of your model, which makes it easier to store, transfer, and deploy.
2. Smaller models also require less memory, which makes them perfect for resource-constrained devices. 
3. Improve inference speed, allowing for faster predictions and real-time applications.
4. Compressed models consume less energy, can be deployed to edge devices such as mobiles, glasses, etc.

## :scissors: Pruning: Trimming the Excess

Model pruning enhances model efficiency by removing unnecessary components, such as weights or entire neurons, from a trained neural network. This process helps reduce the model's size and improves its speed without significantly sacrificing accuracy.

Pruning can be broadly categorized into two types: **unstructured pruning** and **structured pruning**.

### Unstructured Pruning

Unstructured pruning focuses on individual weights within the model. This method involves setting certain weights to zero based on specific criteria, such as their magnitude. By removing these less significant weights, the model remains compact while still retaining its overall functionality. 

### Structured Pruning

In contrast, structured pruning removes larger, predefined groups of parameters, such as entire neurons, filters, or layers. This approach takes into account the architecture of the network and aims to maintain its structural integrity while reducing complexity. 

### Local Pruning
Local pruning refers to the practice of applying pruning techniques at the level of individual layers or components within the model. In this approach, each layer is analyzed independently, and pruning decisions are made based on the characteristics of that specific layer. 

### Global Pruning
In contrast, global pruning considers the entire model as a whole when making pruning decisions. This technique identifies and removes the least significant connections across all layers simultaneously. By doing so, global pruning often achieves better overall performance and efficiency compared to local methods, as it allows for more comprehensive optimization of the network's structure.

Pruning Tutorial [<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab">](https://colab.research.google.com/github/pytorch/tutorials/blob/gh-pages/_downloads/7126bf7beed4c4c3a05bcc2dac8baa3c/pruning_tutorial.ipynb)

## :white_large_square: :white_medium_square: Quantization: Shrinking the Precision

Model quantization reduces the size and computational requirements of neural networks by converting high-precision weights and activations into lower-precision formats.

Different numerical formats are used to represent weights and activations in neural networks. 
- Float32 (FP32): a 32-bit floating point, is the standard representation for real numbers in many machine learning models.
- Bfloat16 (BF16): a 16-bit floating-point format that retains the exponent size of float32 but reduces the number of bits used for the mantissa. This allows it to represent a similar range as float32 but with less precision.
- Int8: an 8-bit integer format that can represent values from [−128,127][−128,127].
- 
Quantization techniques aim to convert high-precision representations (like float32) into lower-precision formats (like int8 or int4) to enhance performance and reduce resource consumption in deep learning models. 

### Quantization Techniques
- **Post-Training Quantization (PTQ)**: PTQ involves quantizing a pre-trained model after its training phase. Common approaches within PTQ include:
    - Parameter Quantization: Reduces the precision of weights and biases.
    - Dynamic Range Quantization: Adjusts the precision of weights based on observed activation ranges.
    - Mixed-Precision Quantization: Combines different precision levels for weights and activations to balance accuracy and efficiency.

- **Quantization-Aware Training (QAT)**: In contrast to PTQ, QAT integrates quantization during the training process. Key aspects include:
    - Activation Quantization: Involves quantizing not just weights but also intermediate activation values during inference.
    - Fake Quantization: Simulates the effects of quantization during training, helping the model adjust accordingly.

There two popular libraries for quantization,

- **GPTQ (Generalized Post-Training Quantization)**: GPTQ employs a mixed quantization strategy using INT4 for weights while keeping activations in higher precision (FP16). 
- **Bitsandbytes**: Bitsandbytes is a library designed for efficient training and inference of large language models. It provides tools for quantizing models, enabling reduced memory consumption and faster processing times. The library supports various quantization techniques, including both PTQ and QAT, making it versatile for different use cases.

## :woman_teacher: :man_student: Distillation: Knowledge Transfer for Efficiency

Distillation is a process of training a smaller, more compact model to mimic the behavior of a larger, more complex model. 

By transferring knowledge from the larger model, distillation enables the creation of highly efficient models without sacrificing performance. This technique has been particularly effective in scenarios where computational resources are limited, such as deploying models on edge devices, smartphones, tablets, etc. A large language model can be distilled into a smaller model that retains most of the original model’s performance while being more lightweight and faster to execute.

Knowledge Distillation Tutorial [<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab">](https://colab.research.google.com/github/pytorch/tutorials/blob/gh-pages/_downloads/a19d8941b0ebb13c102e41c7e24bc5fb/knowledge_distillation_tutorial.ipynb)
