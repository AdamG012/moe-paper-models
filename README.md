---
author: Adam G
title: Papers Setups
---


# Papers Setups

This repository serves as a collection of notable paper experitmental setups. Do note that these could be incomplete or erroneous for some metrics, if so feel free to raise an issue and I will amend it as soon as possible.
Major tasks examined across these papers:
1.  Machine Translation (MT) - tested mainly on datasets like WMT
    (English to French) and BLEU scores are used
2.  Masked Language Modelling (MLM)
3.  Language Modelling (LM)

And as an extra study:

1.  Multitask Downstream tasks

Symbols:

- \*   = Values that are unconfirmed or insinuated from their experiments.
- N/A = Not available (or couldn't find it)

## Model Sizes of Paper Implementations

| Paper                   | Expert Size             | Total Size              | Num Experts (per layer) | Num Layers                |
|-------------------------|-------------------------|-------------------------|---------------------|---------------------------|
| Megablocks              | N/A                     | 839M-13B                | 64                  | 3/6/12                    |
| DeepSpeed-MoE           | 1.3/2.4/8/24/47B        | 52/107/349/1064.9/2024B | 128                 | 24/16/30/40/58            |
| Expert Choice Routing   | 0.145/9.8B              | 1.9/143B                | 64                  | 16                        |
| Task-Level MoE          | 4096 FFN Size           | 533M/13B                | 32/128              | 11                        |
| Hash Layers (vs Switch) | 4096 FFN Size           | 751M/852M/1.28B         | 64/16/128           | 1/5/1                     |
| Hash Layers (vs BASE)   | 100M/33M                | 4.5B                    | 32/3x32             | 1/3                       |
| GShard                  | 8196 FNN Size           | 37/150/600B             | 128/512/2048        | 12/36 (for each num exp)  |
| FasterMoE               | 1024/2048/4096 FFN Size | 13.1/13.7/27.4B         | 64/16/16            | 12/12/24                  |
| ST-MoE                  | 2816/20480              | 4.1/269B                | 32/64               | 6/6 (every 4)             |
| Random Routing          |                         | 20M-200M                | 8/16                | 4/12                      |
| Gating Dropout          |                         | 5.6/10B                 | 128/64              | 12/24                     |
| BASE                    | 135/335/911M            | 1.5/44/117B             | 128                | 1 (BASE Layer)            |
| Switch Transformer      | 768/1024/4096 FFN Size  | 7/26/395/1571B          | 128/128/64/2048     | 12/24/24/15 (Every other) |
| Evo MoE                 | 335M(MT/MLM/LM)         | 1.5(MT)/1.8(MLM LM)     | 4(MT)/16(MLM LM)    | 6(MT)/12(MLM LM)          |
| Stable-MoE              |                         |                         |                     |                           |


## Experimental Setups of Baselines and Hardware

| Paper                   | Baseline                                      | Hardware Requirements | Top-K      | Capacity        |
|-------------------------|-----------------------------------------------|-----------------------|------------|-----------------|
| Megablocks              | Transformer-Base to GPT3-XL (46M to 1.3B)     | 8x A100 80GB          | 1          | 1/1.5/2x        |
| Deepspeed-MoE           | Scalable MoE                                  | 128x A100 80GB        | 2\*        | 2               |
| Expert Choice Routing   | GShard                                        | 512x TPU V4           | N/A\*      | 2\*             |
| Task-Level MoE          | Transformer Base (142M)/Token/Sentence MoE    | 32x TPU V3            | 1          |                 |
| Hash Layers (vs Switch) | Transformer-Base(225/755M)/Switch Transformer | 8 32GB V100           | \*1        |                 |
| Hash Layers (vs BASE)   | BASE Layers                                   | 16 32GB V100          | \*1        |                 |
| GShard                  | GPipe/Base Transformer                        | 128/512/2048x TPU V3  | 2          | 2               |
| FasterMoE               | FastMoE/ GShard/ BASE                         | 16/64x V100           | 2          |                 |
| ST-MoE                  | Dense-L/ T5 XXL/ Switch XXL                   | TPU                   | 2          | 1.25 Cap factor |
| Random Routing          | Thor/Transformer Dense                        | 8x V100               | 1/2/4/8/16 |                 |
| Gating Dropout          | Scalable MoE                                  | 16/64x of V100/A100   | 1          | 1/2(train/test) |
| BASE                    | SMoE and Switch (52B)                         | 8/32/128 32GB V100    |            |                 |
| Switch Transformer      | T5(223M Base/ 739M Large)                     | 32x TPUv3             | 1          |                 |
| Evo MoE                 | Switch/Hash Layers/BASE/StableMoE             | 8x A100               | 1          |                 |
| Stable-MoE              |                                               |                       |            |                 |
|                         |                                               |                       |            |                 |

## Datasets, Citations and Open Source

Highest citation number is taken across Google Scholar and Semantic
scholar

| Paper                   | Dataset (not comprehensive)                       | Batch Size | Open Source  | Citations    |
|-------------------------|---------------------------------------------------|------------|--------------|--------------|
| Megablocks              | The Pile                                          | 512        | N            | 0            |
| Deepspeed-MoE           | Lambada/PIQA/BoolQ/RACE-h/Trivia-QA/WebQS         | 256/512    | Y            | 15/36        |
| Expert Choice Routing   | GLaM                                              | N/A        | N            | 6            |
| Task-Level MoE          | WMT                                               | N/A        | N            | 13           |
| Hash Layers (vs Switch) | Pushshift.io/RoBERTa/Wikitext-103/BST             | 40         | Y (partly)   | 43           |
| Hash Layers (vs BASE)   | Pushshift.io/RoBERTa/Wikitext-103/BST             | 2          | Y (partly)   | 43           |
| GShard                  | Custom Dataset                                    | 4M         | Y (TPU Only) | 305          |
| FasterMoE               | Wiki Text                                         |            | Y            | 22           |
| ST-MoE                  | C4 1.5T                                           | 1M         | Y            | 26           |
| Random Routing          | enwik8/Bookcorpus                                 | 128/256    | Under Review | Under Review |
| Gating Dropout          | WMT/Web-50                                        | 435K       | N            | 1/5          |
| BASE                    | RoBERTa corpus and CC100                          |            | Y            | 64/79        |
| Switch Transformer      | Large C4 Corpus (180B)                            | 1M         | Y            | 525          |
| Evo MoE                 | WMT(MT)/OpenWebText(LM MLM)/Wikipedia/OpenWebText | N/A        | Y            | 11           |
| Stable-MoE              |                                                   |            | Y            | 9            |
|                         |                                                   |            |              |              |
