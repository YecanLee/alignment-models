This release corresponds to the Automatic Alignment Model 1.1.
This new version separates scripts for training the model and for testing in on different functionalities.
Its applications can be regrouped under three major outputs:
1) Best Alignment
2) Top k best alignments
3) All alignments and their corresponding alignment scores, ranked from the best to the worst

# Automatic Alignment Model
Implementation of the automatic alignment model from the paper **"Aligning Actions Across Recipe Graphs"**. In this paper we present two automatic alignment models (base, extended) and a simple baseline (cosine similarity).

*Internal note*: If you are searching for the version of the alignment model implied in our crowdsourcing task, please visit this [private repository](https://github.com/interactive-cookbook/crowdsourcing/tree/main/topk-alignments/alignment-model-topk).

## Requirements
You can find all the requirements in the file `requirement.txt`. Please call `requirement.txt --no-depts` when you install the requirements.
- Python 3.7
- Conllu 4.2.2
- Matplotlib 3.3.2
- Pandas 1.2.3
- Pytorch 1.7.1
- Transformers 4.0.0
- Flair 0.8.0.post1
- AllenNLP 0.9.0

## Usage

Download the corpus from [here](https://github.com/interactive-cookbook/alignment-models/tree/main/data/alignment) into `./alignment-models/data/` folder for reproducing our experiment results. The data should be structured in one directory (/data), containing subdirectories corresponding to the different dishes, each of them including the recipes of the dish regrouped under a /recipes directory, and an "alignments.tsv" file. This file shows the crowsourced golden standard alignments of the correspoding recipes. Additionally, create the results folder where the trained models and their test results will be saved (**Notes:** You can change the hyperparameters and the path names in the file `constants.py`). Per default, the script looks for the following results folders:

Model Name | Saves To
--- | ---
Alignment Model (extended) | `./results1`
Alignment Model (base) | `./results2`
Cosine Similarity Baseline | `./results3`
Naive Model | `./results4`

To reproduce our experimental results, run the following command from this directory:

`python main.py [model_name] --embedding_name [embedding_name]`

where `[model_name]` could be one of the following:
- `Sequence` : Sequential Ordering of Alignments
- `Cosine_similarity` : Cosine model (Baseline)
- `Naive` :  Common Action Pair Heuristics mode (Naive Model)
- `Alignment-no-feature` : Base Alignment model (w/o parent+child nodes)
- `Alignment-with-feature` : Extended Alignment model (with parent+child nodes)

and `[embedding_name]` could be one of the following:
- `bert` : BERT embeddings (default)
- `elmo` : ELMO embeddings

## Results

Our experiment results are as follows:

| Model Name | Accuracy |
| ---------- | :---: |
|Sequential Order | 16.5 |
|Cosine Similarity | 41.5 |
|Naive Model | 52.1 |
| Alignment Model (base) | 66.3 |
| Alignment Model (extended) | **72.4** |

Both the base and the extended Alignment models were trained for 10 folds each with 40 epochs.


