---
layout: model
title: English RobertaForMaskedLM Base Cased model (from model-attribution-challenge)
author: John Snow Labs
name: roberta_embeddings_model_attribution_challenge_base
date: 2022-12-12
tags: [en, open_source, roberta_embeddings, robertaformaskedlm]
task: Embeddings
language: en
nav_key: models
edition: Spark NLP 4.2.4
spark_version: 3.0
supported: true
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained RobertaForMaskedLM model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP. `roberta-base` is a English model originally trained by `model-attribution-challenge`.

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/roberta_embeddings_model_attribution_challenge_base_en_4.2.4_3.0_1670859033776.zip){:.button.button-orange.button-orange-trans.arr.button-icon}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/public/models/roberta_embeddings_model_attribution_challenge_base_en_4.2.4_3.0_1670859033776.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = DocumentAssembler() \
    .setInputCols(["text"]) \
    .setOutputCols("document")

tokenizer = Tokenizer() \
    .setInputCols("document") \
    .setOutputCol("token")

roberta_loaded = RoBertaEmbeddings.pretrained("roberta_embeddings_model_attribution_challenge_base","en") \
    .setInputCols(["document", "token"]) \
    .setOutputCol("embeddings") \
    .setCaseSensitive(True)
    
pipeline = Pipeline(stages=[documentAssembler, tokenizer, roberta_loaded])

data = spark.createDataFrame([["I love Spark NLP"]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val documentAssembler = new DocumentAssembler() 
    .setInputCols(Array("text")) 
    .setOutputCols(Array("document"))
      
val tokenizer = new Tokenizer()
    .setInputCols("document")
    .setOutputCol("token")
 
val roberta_loaded = RoBertaEmbeddings.pretrained("roberta_embeddings_model_attribution_challenge_base","en") 
    .setInputCols(Array("document", "token"))
    .setOutputCol("embeddings")
    .setCaseSensitive(true)    
   
val pipeline = new Pipeline().setStages(Array(documentAssembler, tokenizer, roberta_loaded))

val data = Seq("I love Spark NLP").toDS.toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|roberta_embeddings_model_attribution_challenge_base|
|Compatibility:|Spark NLP 4.2.4+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[sentence, token]|
|Output Labels:|[embeddings]|
|Language:|en|
|Size:|300.9 MB|
|Case sensitive:|true|

## References

- https://huggingface.co/model-attribution-challenge/roberta-base
- https://arxiv.org/abs/1907.11692
- https://github.com/pytorch/fairseq/tree/master/examples/roberta
- https://yknzhu.wixsite.com/mbweb
- https://en.wikipedia.org/wiki/English_Wikipedia
- https://commoncrawl.org/2016/10/news-dataset-available/
- https://github.com/jcpeterson/openwebtext
- https://arxiv.org/abs/1806.02847