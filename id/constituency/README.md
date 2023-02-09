# ICON: A Large-Scale Benchmark Constituency Treebank for the Indonesian Language

This repository contains the ICON dataset for constituency parsing in Indonesian.

## Bracketed Format

The text files (train/dev/test) contain the constituency parse trees in a compact format called bracketed notation.
An example is as follows:

`(S (NP (NNP Sahrul)) (VP (VBT mengawali) (NP (NNO karier) (PRK nya)) (PP (PPO dari) (NP (NNO dunia) (NNO model)))) (PUN .))`

The tags closest to the word tokens are POS tags and the tags surrounding them are phrase-level or clause-level tags.

In the example above, the token `Sahrul` is labeled as `(NP (NNP Sahrul))`, meaning that it is a proper noun (`NNP`) and part of a noun phrase (`NP`). The noun phrase is in turn part of main clause `S` which also contains a verb phrase (`VP`) and a punctuation (`PUN`).

## Model Training/Evaluation

We trained the Berkeley Neural Parser on the ICON treebank. If you wish to train your own parser, please follow the instructions found under `Training` on Berkeley Neural Parser's GitHub repository (https://github.com/nikitakit/self-attentive-parser).

For the best configuration, please run the training with the following command:

```
python src/main.py train \
--train-path train.txt --dev-path dev.txt --test-path test.txt \
--pretrained-model spanbert_indolem_base_checkpoint_best \
--checks-per-epoch 4 --numpy-seed 1234 --batch-size 32 --learning-rate 5e-05 \
--subbatch-max-tokens 1500 --use-pretrained --d-char-emb 64 --char-lstm-input-dropout 0.2 \
--use-encoder --encoder-max-len 512 --num-layers 8 --num-heads 8 \
--d-kv 64 --d-ff 2048 --d-model 1024 \
--morpho-emb-dropout 0.2 --attention-dropout 0.2 --relu-dropout 0.1 --residual-dropout 0.2 \
--predict-tags
```
`--pretrained-model` can be a reference to a model name on HuggingFace, such as `xlm-roberta-base`.

## License

The ICON dataset is made available under the CC BY-SA 4.0 License.

Shield: [![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg 