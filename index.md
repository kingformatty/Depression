# Project Summary

This project contains two parts
1. Depression Classification
2. Speaker Diarization: <br/>
        Speaker Diarization experiments are implemented for the prupose to obtaining more data from the raw audio to alleviate the work for frame level speaker annotation. More specific, the performance is not only evaluated based on Diarization Error Rate (DER), but also based on the performance on how well the patient audio can be extracted with high confidence.

Notation: Since the final target of this project is to detect the depression emotion of patient. Therefore, evaluate the confidence of extract patient audio is crucial for the model, even more important than DER. For patient analysis, we use precision, recall and F1-score to evaluate the model about the performance on extract high-confidence patient audio. Precision is the duration of correct detected patient audio divided by the detected patient audio. Recall is the duration of correct detected patient audio divided by the total duration in test set. And F1-score is the balanced metrics for Precision and Recall. 
        
        
# Section
## 1. Depression Classification


## 2. Speaker Diarization

### 2.1. Pipeline Finetuning
```markdown


```
### 2.2. Block Finetuning

Since the conventional speaker diarization pipeline contains blocks as speaker activity detection, speaker change detection, and speaker embedding block. This approach is to use the groundtruth data to finetune the model pretrained with DIHARD dataset for each block separately. And then do the pipeline finetuning jointly at the final stage. 
```markdown
Diarization Results
| Exp                    | DER           | False Alarm  | Miss Detected | Confusion |
| ---------------------- |:-------------:| ------------:|---------------|-----------|
| Baseline               | 66.86         |              |               |           |
| Pipeline Finetune      | 41.97         | 8.99         | 10.95         | 22.02     |
| Block Finetune         | 43.8          | 10.13        | 9.13          | 24.54     | 

``` 
```markdown
Patient Analysis
| Exp                    | Precision     | Recall       | Fscore        |  
| ---------------------- |:-------------:| ------------:|---------------|
| Pipeline Finetune      | 63.88         | 24.66        | 35.58         |
| Block Finetune         | 47.44         | 33.6         | 39.34         | 

``` 

### 2.4. Two Centriods AHC Reformulation
Unlike conventional diarization task that the system has to determine the number of speaker by itself. In this project, each sample is a two-speaker utterance. Thus, we restrict the number of centriod to be 2 to simplify the problem.

```markdown
| Exp                    | DER           | False Alarm  | Miss Detected | Confusion |
| ---------------------- |:-------------:| ------------:|---------------|-----------|
| Baseline               | 66.86         |              |               |           |
| Block Finetune         | 43.8          | 10.13        | 9.13          | 24.54     | 
| Block Finetune AHC     | 43.75         | 5.19         | 20.63         | 17.93     |
| Block Finetune AHC TFS | 39.88         | 4.78         | 16.16         | 18.94     |     

``` 
```markdown
Patient Analysis
| Exp                    | Precision     | Recall       | Fscore        |  
| ---------------------- |:-------------:| ------------:|---------------|
| Block Finetune         | 47.44         | 33.6         | 39.34         | 
| Block Finetune AHC     | 75.06         | 13.2         | 22.45         |
| Block Finetune AHC TFS | 71.53         | 14.3         | 23.85         |

```

### 2.4. Mandrain Corpus Embedding Pretraining
Since DIHARD pretrained model is based on English, to mitigate the language mismatch, we retrain the embedding model on CN-Celeb dataset (about 300 hours), and keep the other two tuned blocks to be identical.

```markdown
| Exp                    | DER           | False Alarm  | Miss Detected | Confusion |
| ---------------------- |:-------------:| ------------:|---------------|-----------|
| Baseline               | 66.86         |              |               |           |
| Block Finetune         | 43.8          | 10.13        | 9.13          | 24.54     | 
| Block Finetune AHC     | 43.75         | 5.19         | 20.63         | 17.93     |
| + CN_pretrain          | 44.14         | 11.62        | 7.98          | 24.54     |
| + Finetune             | 44.91         | 2.77         | 30.36         | 11.78     |
```

```markdown
Patient Analysis
| Exp                    | Precision     | Recall       | Fscore        |  
| ---------------------- |:-------------:| ------------:|---------------|
| Block Finetune         | 47.44         | 33.6         | 39.34         | 
| Block Finetune AHC     | 75.06         | 13.2         | 22.45         |
| + CN_pretrain          | 81.78         | 17.4         | 28.80         | 
| + Finetune             | 78.92         | 36.21        | 49.64         |
```

### 2.5. Doc vs Patient Binary Classification Reformulation
Step further from the centroid-restrict clustering, we come up with a simplier binary classification model to replace the AHC clustering. Performance is evaluated purly on the patient perspective, i.e. how well the model can extract the patient audio with relatively higher confidence.

```markdown
Patient Analysis
| Exp                    | threshold     | Precision    | Recall        | Fscore        |  
| ---------------------- |:-------------:| ------------:|---------------|---------------|
| Logistic Regression    |  0.5          | 34.57        | 21.6          | 26.59         | 
|                        |  0.8          | 31.09        | 2.49          | 4.56          |
|                        |  0.98         | 96.62        | 0.37          | 0.74          | 
| ---------------------- |:-------------:| ------------:|---------------|---------------|
| Quadratic DA           |  0.5          | 47.44        | 43.36         | 42.63         | 
|                        |  0.8          | 75.06        | 33.92         | 36.7          |
|                        |  0.98         | 81.78        | 31.56         | 34.83         | 
| ---------------------- |:-------------:| ------------:|---------------|---------------|
| KNN                    |               | 47.44        | 44.85         | 42.17         | 
```

The Precision vs Recall Curve and F1 vs Threshold Curve are as shown below in Figure.
(https://github.com/kingformatty/Depression/edit/gh-pages/pr.png)




### Contact

Jinhan Wang: wang7875@g.ucla.edu
