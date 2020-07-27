# English2Gloss NMT
Translates english sentences to ASL gloss sentences using a transformer model.

# Based on: Attention is all you need: A Pytorch Implementation
https://github.com/jadore801120/attention-is-all-you-need-pytorch

# Requirement
- python 3.4+
- pytorch 1.3.1
- torchtext 0.4.0
- spacy 2.2.2+
- tqdm
- dill
- numpy


# Usage

## WMT'16 Multimodal Translation: de-en

An example of training for the WMT'16 Multimodal Translation task (http://www.statmt.org/wmt16/multimodal-task.html).

### 0) Download the spacy language model.
```bash
python -m spacy download en
```

### 1) Preprocess the data with torchtext and spacy.
```bash
python preprocess.py -lang_src en -lang_trg en -share_vocab -save_data eng2asl_shr.pkl
```

### 2) Train the model
```bash
python train.py -data_pkl eng2asl_shr.pkl -log eng2asl_shr -embs_share_weight -proj_share_weight -label_smoothing -save_model trained -b 64 -warmup 128000 -epoch 200
```

### 3) Translate using the model
```bash
python translate.py -data_pkl eng2asl_shr.pkl -model trained.chkpt -input translate_src.txt -output prediction.txt

```
