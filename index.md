# Project Summary

This project contains two parts
1. Depression Classification
2. Speaker Diarization: <br/>
        Speaker Diarization experiments are implemented for the prupose to obtaining more data from the raw audio to alleviate the work for frmae level speaker annotation. 

# Section
## 1. Depression Classification


## 2. Speaker Diarization

### 2.1. Pipeline Finetuning
```markdown


```
### 2.2. Block Finetuning

Since the conventional speaker diarization pipeline contains blocks as speaker activity detection, speaker change detection, and speaker embedding block. This approach is to use the groundtruth data to finetune the model pretrained with DIHARD dataset for each block separately. And then do the pipeline finetuning jointly at the final stage. 
```markdown

``` 

### 2.4. Two Centriods AHC Reformulation
```markdown

``` 

### 2.4. Mandrain Corpus Embedding Pretraining
```markdown

``` 
### 2.5. Doc vs Patient Binary Classification Reformulation
```markdown

```


```markdown
Syntax highlighted code block


# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/kingformatty/Depression/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
