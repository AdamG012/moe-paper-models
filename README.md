---
author: Adam G
title: MoE Papers Experimental Setups
---

# Mixture of Experts (MoE) Paper Experimental Setups

This repository serves as a collection of notable paper experitmental setups. Do note that these could be incomplete or erroneous for some metrics, if so feel free to raise an issue and I will amend it as soon as possible.

Major tasks examined across these papers:

1.  Machine Translation (MT) - tested mainly on datasets like WMT (English to French) and BLEU scores are used
2.  Masked Language Modelling (MLM)
3.  Language Modelling (LM)


<a id="orgc8e966a"></a>

## Model Sizes of Paper Implementations

| Paper                                                              | Year    | Expert Size             | Total Size                      | Num Exp (per layer)                     | Num Layers                                  |
| [Megablocks](https://arxiv.org/abs/2211.15841)                     | 11/2022 | N/A                     | 839M-13B                        | 64                                      | 3/6/12                                      |
| [Deepspeed-MoE](https://arxiv.org/abs/2201.05596)                  | 01/2022 | 1.3/2.4/8/24/47B        | 52/107/349/1064.9/2024B         | 128                                     | 24/16/30/40/58                              |
| [Deepspeed-MoE](https://arxiv.org/abs/2201.05596)                  | 01/2022 | 1.3/2.4/8/24/47B        | 52/107/349/1064.9/2024B         | 128                                     | 24/16/30/40/58                              |
| [Expert Choice Routing](https://arxiv.org/abs/2202.09368)          | 02/2022 | 0.145/9.8B              | 1.9/143B                        | 64                                      | 16                                          |
| [Task-Level MoE](https://arxiv.org/abs/2110.03742)                 | 09/2022 | 4096 FFN Size           | 533M/13B                        | 32/128                                  | 11                                          |
| [Hash Layers (vs Switch)](https://arxiv.org/abs/2106.04426)        | 06/2021 | 4096 FFN Size           | 751M/852M/1.28B                 | 64/16/128                               | 1/5/1                                       |
| [Hash Layers (vs BASE)](https://arxiv.org/abs/2106.04426)          | 06/2021 | 100M/33M                | 4.5B                            | 32/3x32                                 | 1/3                                         |
| [GShard](https://arxiv.org/abs/2006.16668)                         | 06/2020 | 8196 FNN Size           | 37/150/600B                     | 128/512/2048                            | 12/36 (for each num exp)                    |
| [FasterMoE](https://dl.acm.org/doi/pdf/10.1145/3503221.3508418)    | 03/2022 | 1024/2048/4096 FFN Size | 13.1/13.7/27.4B                 | 64/16/16                                | 12/12/24                                    |
| [ST-MoE](https://arxiv.org/abs/2202.08906)                         | 02/2022 | 2816/20480              | 4.1/269B                        | 32/64                                   | 6/6 (every 4)                               |
| [Random Routing](https://openreview.net/pdf?id=w1hwFUb_81)         | 09/2022 |                         | 20M-200M                        | 8/16                                    | 4/12                                        |
| [Gating Dropout](https://arxiv.org/abs/2205.14336)                 | 05/2022 |                         | 5.6/10B                         | 128/64                                  | 12/24                                       |
| [BASE Layers](https://arxiv.org/abs/2103.16716)                    | 03/2021 | 135/335/911M            | 1.5/44/117B                     | 128?                                    | 1 (BASE Layer)                              |
| [Switch Transformer](https://arxiv.org/abs/2101.03961)             | 01/2021 | 768/1024/4096 FFN Size  | 7/26/395/1571B                  | 128/128/64/2048                         | 12/24/24/15 (Every other)                   |
| [Evo MoE](https://arxiv.org/abs/2112.14397)                        | 12/2021 | 335M(MT/MLM/LM)         | 1.5(MT)/1.8(MLM LM)             | 4(MT)/16(MLM  LM)                       | 6(MT)/12(MLM LM)                            |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (LM)                | 04/2022 | 3072/4096 FFN Size      | 454M/3.22B                      | 32/64                                   | 1/1                                         |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (MT)                | 04/2022 | 2048 FFN Size           | 480M                            | 32                                      | 2                                           |
| [Outrageously Large MoEs](https://arxiv.org/abs/1701.06538v1) (LM) | 01/2017 | 1M(dims=1024x512)       | 0.8/0.9/1.1/1.1/1.9/5.1         | 4/32/256/256/1024/4096                  | 1                                           |
| Outrageously Large MoEs (LM-Large)                                 | 01/2017 | 1M                      | 0.1/0.4/1.2/4.4/17.3/68.9/137.7 | 32 & 256/1024/4096/16384/65536/131072-h | 1                                           |
| Outrageously Large MoEs (MT)                                       | 01/2017 | 2M                      | 8.7B                            | 32 & 512/2048-h                         | 2 (one between stacked encoder and decoder) |
| Outrageously Large MoEs (MTMT)                                     | 01/2017 | 8192 FFN Size           | 8.7B                            | 512                                     | 2                                           |
| [NLLB](https://arxiv.org/abs/2207.04672)                           | 07/2022 | 8192 FFN Size/33.6M     | 54.5B/51.6B Expert Size         | 128                                     | 6 Exp Layers                                |
| [Memory Efficient NLLB](https://arxiv.org/abs/2212.09811)          | 12/2022 | 8192 FFN Size/33.6M     | ~10.32B assuming 80% pruning    | ~24 per layer, 288 overall              | 6 Exp Layers                                |

\\\* = Values that are unconfirmed or insinuated from their experiments.


<a id="org95d3e84"></a>

## Experimental Setups of Baselines and Hardware

For hardware requirements, slashes denote different configurations.

| Paper                                                              | Baseline                                                  | Hardware Requirements | Memory                              | Top-K            | Capacity        |
| [Megablocks](https://arxiv.org/abs/2211.15841)                     | Transformer-Base to GPT3-XL (46M to 1.3B)                 | 8x A100 80GB          |                                     | 1                | 1/1.5/2x        |
| [Deepspeed-MoE](https://arxiv.org/abs/2201.05596)                  | Scalable MoE                                              | 128x A100 80GB        |                                     | 2\*              | 2               |
| [Expert Choice Routing](https://arxiv.org/abs/2202.09368)          | GShard                                                    | 512x TPU V4           |                                     | N/A\*            | 2\*             |
| [Task-Level MoE](https://arxiv.org/abs/2110.03742)                 | Transformer Base (142M)/Token/Sentence MoE                | 32x TPU V3            |                                     | 1                |                 |
| [Hash Layers (vs Switch)](https://arxiv.org/abs/2106.04426)        | Transformer-Base(225/755M)/Switch Transformer             | 8 32GB V100           |                                     | \*1              |                 |
| [Hash Layers (vs BASE)](https://arxiv.org/abs/2106.04426)          | BASE Layers                                               | 16 32GB V100          |                                     | \*1              |                 |
| [GShard](https://arxiv.org/abs/2006.16668)                         | GPipe/Base Transformer                                    | 128/512/2048x TPU V3  |                                     | 2                | 2               |
| [FasterMoE](https://dl.acm.org/doi/pdf/10.1145/3503221.3508418)    | FastMoE/ GShard/ BASE                                     | 16/64x V100           |                                     | 2                |                 |
| [ST-MoE](https://arxiv.org/abs/2202.08906)                         | Dense-L/ T5 XXL/ Switch XXL                               | TPU                   |                                     | 2                | 1.25 Cap factor |
| [Random Routing](https://openreview.net/pdf?id=w1hwFUb_81)         | Thor/Transformer Dense                                    | 8x V100               |                                     | 1/2/4/8/16       |                 |
| [Gating Dropout](https://arxiv.org/abs/2205.14336)                 | Scalable MoE                                              | 16/64x of V100/A100   |                                     | 1                | 1/2(train/test) |
| [BASE Layers](https://arxiv.org/abs/2103.16716)                    | SMoE and Switch (52B)                                     | 8/32/128 32GB V100    |                                     |                  |                 |
| [Switch Transformer](https://arxiv.org/abs/2101.03961)             | T5(223M Base/ 739M Large)                                 | 32x TPUv3             |                                     | 1                |                 |
| [Evo MoE](https://arxiv.org/abs/2112.14397)                        | Switch/Hash Layers/BASE/StableMoE                         | 8x A100               |                                     | 1                |                 |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (LM)                | Switch Transformer/BASE Layer/Hash Layer/Transformer-Base | ?x V100 GPUs          |                                     | 1                | 1 (from Switch) |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (MT)                | Transformer-Base and Large/BASE Layer/Hash Layer/Switch   | ?x V100 GPUs          |                                     | 1                | 1               |
| [Outrageously Large MoEs](https://arxiv.org/abs/1701.06538v1) (LM) | MoE-1 Wide & Deep/ 4xLSTM-512/LSTM-2048 & 8192            | 4-16x k40s            |                                     | 4 or 2 for MoE-h |                 |
| Outrageously Large MoEs (LM-Large)                                 | MoE-1 Wide & Deep/ 4xLSTM-512/LSTM-2048 & 8192            | 32/64/128x k40s       |                                     | 4 or 2 for MoE-h |                 |
| Outrageously Large MoEs (MT)                                       | GNMT/PBMT/LSTM-6/DeepAtt                                  | 64 k40s               |                                     | 4 or 2 for MoE-h |                 |
| Outrageously Large MoEs (MTMT)                                     | GNMT-Mono/GNMT-Multi                                      | 64 k40s               |                                     | 2                |                 |
| [NLLB](https://arxiv.org/abs/2207.04672)                           |                                                           |                       | 101.6GiB/ each GPU holds one expert |                  |                 |
| [Memory Efficient NLLB](https://arxiv.org/abs/2212.09811)          | 3.3B NLLB-Dense/NLLB-200 54.5B                            | 1/4x V100 GPUs        |                                     |                  |                 |


<a id="orgb8ad090"></a>

## Datasets, Citations and Open Source

Highest citation number is taken across Google Scholar and Semantic scholar

| Paper                                                              | Dataset                                                                   | Batch Size      | Open Source               | Citations      | Notes                                                                                                                                                                          |
| [Megablocks](https://arxiv.org/abs/2211.15841)                     | The Pile                                                                  | 512             | N                         | 0              |                                                                                                                                                                                |
| [Deepspeed-MoE](https://arxiv.org/abs/2201.05596)                  | Lambada/PIQA/BoolQ/RACE-h/Trivia-QA/WebQS                                 | 256/512         | Y                         | 15/36          |                                                                                                                                                                                |
| [Expert Choice Routing](https://arxiv.org/abs/2202.09368)          | GLaM                                                                      | N/A             | N                         | 6              |                                                                                                                                                                                |
| [Task-Level MoE](https://arxiv.org/abs/2110.03742)                 | WMT                                                                       | N/A             | N                         | 13             |                                                                                                                                                                                |
| [Hash Layers (vs Switch)](https://arxiv.org/abs/2106.04426)        | Pushshift.io/RoBERTa/Wikitext-103/BST                                     | 40              | Y (partly)                | 43             |                                                                                                                                                                                |
| [Hash Layers (vs BASE)](https://arxiv.org/abs/2106.04426)          | Pushshift.io/RoBERTa/Wikitext-103/BST                                     | 2               | Y (partly)                | 43             |                                                                                                                                                                                |
| [GShard](https://arxiv.org/abs/2006.16668)                         | Custom Dataset                                                            | 4M              | Y (TPU Only)              | 305            |                                                                                                                                                                                |
| [FasterMoE](https://dl.acm.org/doi/pdf/10.1145/3503221.3508418)    | Wiki Text                                                                 |                 | Y                         | 22             |                                                                                                                                                                                |
| [ST-MoE](https://arxiv.org/abs/2202.08906)                         | C4 1.5T                                                                   | 1M              | Y                         | 26             |                                                                                                                                                                                |
| [Random Routing](https://openreview.net/pdf?id=w1hwFUb_81)         | enwik8/Bookcorpus                                                         | 128/256         | Under Review              | Under Review   |                                                                                                                                                                                |
| [Gating Dropout](https://arxiv.org/abs/2205.14336)                 | WMT/Web-50                                                                | 435K            | N                         | 1/5            |                                                                                                                                                                                |
| [BASE Layers](https://arxiv.org/abs/2103.16716)                    | RoBERTa corpus and CC100                                                  |                 | Y                         | 64/79          |                                                                                                                                                                                |
| [Switch Transformer](https://arxiv.org/abs/2101.03961)             | Large C4 Corpus (180B)                                                    | 1M              | Y                         | 525            |                                                                                                                                                                                |
| [Evo MoE](https://arxiv.org/abs/2112.14397)                        | WMT(MT)/OpenWebText(LM MLM)/Wikipedia/OpenWebText                         | N/A             | Y                         | 11             |                                                                                                                                                                                |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (LM)                | RoBERTa and CC100                                                         | 512K            | Y                         | 9              |                                                                                                                                                                                |
| [Stable-MoE](https://arxiv.org/abs/2204.08396) (MT)                | WMT                                                                       | 512K            | Y                         | 9              |                                                                                                                                                                                |
| [Outrageously Large MoEs](https://arxiv.org/abs/1701.06538v1) (LM) | 1B word benchmark                                                         | ?               | N(but has been recreated) | 1117/1050      | Uses MoE Layer between two LSTMS. 8.4/37.8/272.9/1079/4303M.                                                                                                                   |
| Outrageously Large MoEs (LM-Large)                                 | 100 Billion Google Corpus                                                 | 2.5M            | &ldquo;&rdquo;            | &ldquo;&rdquo; | Fit up to 1 Billion parameters per GPU. The 64 and 128 GPU tests  are for the last two expert models                                                                           |
| Outrageously Large MoEs (MT)                                       | WMT                                                                       | ?               | &ldquo;&rdquo;            | &ldquo;&rdquo; | Fit up to 1 Billion parameters per GPU.                                                                                                                                        |
| Outrageously Large MoEs (MTMT)                                     | CoRR                                                                      | 1M(16K per GPU) | &ldquo;&rdquo;            | &ldquo;&rdquo; |                                                                                                                                                                                |
| [NLLB](https://arxiv.org/abs/2207.04672)                           | Flores-200(Eval)/LID curated data/Paracrawl and CommonCrawl (Monolingual) | 16K             | Y                         | 26/49          | Every fourth layer is an MoE layer.                                                                                                                                            |
| [Memory Efficient NLLB](https://arxiv.org/abs/2212.09811)          | Flores-200(Eval)/                                                         | 16K             | N                         | 0              | Releasing some results such as experts pruned etc Every fourth FFN sublayer is replaced with an MoE layer. NLLB-200 requires 4x32 V100s to run. This usesthe 80% pruned model. |
