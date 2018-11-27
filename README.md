## This is the team project of CSCE 638 : QA system with SQuAD dataet

---
## To start with
1. Download datasets(run in dataset/):
```
./get_data.bash
```
2. Download pretrained model to encode english sentences:
```
curl -Lo encoder/infersent.allnli.pickle https://s3.amazonaws.com/senteval/infersent/infersent.allnli.pickle
```

3. Start from create_emb.ipynb, note that `textblob` ,`spacy` and `torch` packages are required.

4. To implement question type detection, we used `StanfordPOSTagger`. It is a tagger library written in Java, you can download it from [here](https://nlp.stanford.edu/software/tagger.shtml), then please follow this [link](https://blog.sicara.com/train-ner-model-with-nltk-stanford-tagger-english-french-german-6d90573a9486) to implement the configuration. (Although this link is for StanfordNERTagger, the configuration is the same for StanfordPOSTagger.)

5. For answer extraction, we used UIUC's [ccg-nlpy](https://github.com/CogComp/cogcomp-nlp), it has an API called `get_ner_ontonotes()` to get tags based on Ontonote corpus. Here is a [demo](http://macniece.seas.upenn.edu:4004/).

## Possible Errors and Solutions
1. In `create_emb.ipynb`, you may encounter: `OSError: [E050] Can't find model 'en'. It doesn't seem to be a shortcut link, a Python package or a valid path to a data directory.` --- <b>Solution:</b> change `en_nlp = spacy.load('en')` to `en_nlp = spacy.load('en_core_web_sm')`

2. In this project, we used InferSent as sentence embeddings method, please refer to this [link](https://github.com/facebookresearch/InferSent) to get the dataset and related files. <i>(Note: If the download speed of GloVe dataset is slow (around 400k/s), don't worry. It's normal.)</i>

3. Also, In `create_emb.ipynb`, you may encounter `UnicodeDecodeError` while building vocabulary, please refer to this [link](https://github.com/facebookresearch/InferSent/issues/50) to modify encoder/models.py by by adding `encoding='utf-8'`

4. ccg-nlpy installation. The installation of this package can be found in the demo link above. If you encounter `JDK_HOME/JRE_HOME not determined` when installing `pyjnius`, please first check if you have `JDK_HOME/JRE_HOME` environment variable. If it still doesn't work, install `pyjnius` in conda, and then install `ccg-nlpy`. If you have any questions, contact me (Weitong Feng - harry08010@tamu.edu).

## About the project

1. create_emb.ipynb create an embeddings of senteces in the context and questions. create_emb-wiki-pipeline.ipynb create the embeddings for question in Squad dataset and contexts from wikipedia. create_emb-wiki-custom-input.ipynb create embeddings for custom questions and corresponding wikipedia page and also perform the unsupervised learning task as descrbed below.

2. unsupervised.ipynb basically calcuate the disntance between the embeddings of questions and contexts and find the most similar sentence based metrics like cosine similarity and so on. unsupervised-wiki.ipynb do the same task except the context is form wikipedia.

3. Folder InferSent2 contains the result trained by fastText dataset.If you have any questions, contact me (Shutong Jiao - stjiao13@tamu.edu).


