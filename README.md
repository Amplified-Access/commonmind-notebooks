# CommonMind notebooks

The training and evaluation notebooks behind [CommonMind](https://thecommonmind.org)'s published models. Each notebook here is the run that produced the released model, not an earlier or later experiment. The notebooks were run on Kaggle; the links below go to the original Kaggle notebooks.

## Swahili-gemma-1b-it

[Hugging Face](https://huggingface.co/AmplifiedAccess/Swahili-gemma-1b-it) · [Kaggle](https://www.kaggle.com/models/amplifiedaccess/swahili-gemma-1b-it) · Gemma Terms of Use + non-commercial

| Notebook | What it does | Kaggle source |
|---|---|---|
| [00-baseline-gemma-3-1b-it](swahili-gemma-1b-it/00-baseline-gemma-3-1b-it.ipynb) | Scores the untuned base model on FLORES-200 (BLEU 0.41, chrF++ 14.28) | [amplifiedaccess/baseline-untrained-gemma-3-1b-it](https://www.kaggle.com/code/amplifiedaccess/baseline-untrained-gemma-3-1b-it) |
| [01-continued-pretraining](swahili-gemma-1b-it/01-continued-pretraining.ipynb) | Stage 1: continued pretraining (QLoRA) on Swahili text from JamiiForums ([AlexLeoTz/jamiiforums-2b](https://huggingface.co/datasets/AlexLeoTz/swahili_large_corpus_mini)) and [Inkuba-Mono](https://huggingface.co/datasets/lelapa/Inkuba-Mono) | [gracenoble/swahili-finetune-1](https://www.kaggle.com/code/gracenoble/swahili-finetune-1) |
| [02-merge-cpt-adapter](swahili-gemma-1b-it/02-merge-cpt-adapter.ipynb) | Merges the stage 1 adapter into full weights | [gracenoble/stage-1-merge](https://www.kaggle.com/code/gracenoble/stage-1-merge) |
| [03-instruction-tuning](swahili-gemma-1b-it/03-instruction-tuning.ipynb) | Stage 2: instruction tuning on 159,311 examples, then merge and evaluate (BLEU 28.86, chrF++ 54.77) | [gracenoble/stage2-sft-plus](https://www.kaggle.com/code/gracenoble/stage2-sft-plus) |
| [04-quickstart](swahili-gemma-1b-it/04-quickstart.ipynb) | Loads the released model and translates | [amplifiedaccess/swahili-gemma-1b-it-quickstart](https://www.kaggle.com/code/amplifiedaccess/swahili-gemma-1b-it-quickstart) |

The released weights are byte-identical to the output of `03-instruction-tuning` (`model.safetensors`, SHA-256 prefix `4f3031b5afd36533`).

## Swahili-nllb

| Notebook | Model | Kaggle source |
|---|---|---|
| [swahili-nllb-1.3b](swahili-nllb/swahili-nllb-1.3b.ipynb) | [Swahili-nllb-1.3b](https://huggingface.co/AmplifiedAccess/Swahili-nllb-1.3b): LoRA on NLLB-200 1.3B (BLEU 38.74, chrF++ 63.37) | [gracenoble/swahili-nllb-fine-tune](https://www.kaggle.com/code/gracenoble/swahili-nllb-fine-tune) |
| [swahili-nllb-600m](swahili-nllb/swahili-nllb-600m.ipynb) | [Swahili-nllb-600m](https://huggingface.co/AmplifiedAccess/Swahili-nllb-600m): LoRA on NLLB-200 600M (BLEU 35.97, chrF++ 61.26) | [amplifiedaccess/swahili-nllb-fine-tune-600m](https://www.kaggle.com/code/amplifiedaccess/swahili-nllb-fine-tune-600m) |

Both models are CC BY-NC 4.0. The released adapters are byte-identical to these notebooks' outputs.

## Luganda-gemma-1b-it

[Hugging Face](https://huggingface.co/AmplifiedAccess/Luganda-gemma-1b-it) · [Kaggle](https://www.kaggle.com/models/amplifiedaccess/luganda-gemma-1b-it) · Gemma Terms of Use

| Notebook | What it does | Source |
|---|---|---|
| [01-prepare-data](luganda-gemma-1b-it/01-prepare-data.ipynb) | Builds the training set from SALT and the Kimera English–Luganda corpus: 42,019 clean pairs, 94,542 / 5,252 / 5,253 train / validation / test examples | `luganda-ai` repository |
| [02-finetune](luganda-gemma-1b-it/02-finetune.ipynb) | QLoRA fine-tune of Gemma 3 1B IT and evaluation (BLEU 13.85, chrF++ 46.59 on 100 held-out examples) | [amplifiedaccess/luganda-finetune](https://www.kaggle.com/code/amplifiedaccess/luganda-finetune) |

## Benchmarks

| Notebook | What it does | Kaggle source |
|---|---|---|
| [crane-swahili-gemma-baseline](benchmarks/crane-swahili-gemma-baseline.ipynb) | Scores CraneAILabs Swahili-Gemma-1B on FLORES-200, the reference (BLEU 27.6, chrF++ 56.8) our Swahili models are compared against | [gracenoble/stage0-baseline-benchmark](https://www.kaggle.com/code/gracenoble/stage0-baseline-benchmark) |

## Running the notebooks

They are written for Kaggle GPU notebooks. Add a Kaggle secret named `HF_TOKEN` with a read token for Hugging Face; `google/gemma-3-1b-it` is a gated model, so the token's account must have accepted Gemma's terms. Notebooks that push to the Hugging Face Hub need a token with write access to the target repository.

## Data and licenses

The notebooks download their training data from the original publishers. Each dataset keeps its own license; the model cards list them in their "Training data and licenses" sections. This repository does not redistribute any training data.

The code in this repository is licensed under the [Apache License 2.0](LICENSE).
