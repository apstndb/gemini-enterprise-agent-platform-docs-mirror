---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/pytorch-efficient-training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/pytorch-efficient-training
title: Efficient PyTorch training with cloud data
description: Advice regarding efficient PyTorch training with cloud data
data_source: docs.cloud.google.com
---

Agent Platform Neural Architecture Search has no requirements describing how to design your trainers. Therefore, choose any training frameworks to build the trainer.

For PyTorch training with large amounts of data, the best practice is to use the distributed training paradigm and to read data from Cloud Storage. Check out the blog post [Efficient PyTorch training with Agent Platform Neural Architecture Search](https://cloud.google.com/blog/products/ai-machine-learning/efficient-pytorch-training-with-vertex-ai) for methods to improve the training performance. You can see an overall 6x performance improvement with data on Cloud Storage using `WebDataset` and choosing `DistributedDataParallel` or `FullyShardedDataParallel` distributed training strategies. The training performance using data on Cloud Storage is similar to the training performance using data on a local disk.

The prebuilt [MNasNet classification example](https://github.com/google/vertex-ai-nas/blob/main/pytorch/classification/cloud_search_main.py) has incorporated these methods into its training pipeline.
