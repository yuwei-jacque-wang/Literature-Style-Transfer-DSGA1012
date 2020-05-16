# Literature Style Transfer


This is code implementation of the final project of DS-GA 1012:
```
Text-style Transformation from 19th-Century Literature to Modern Language
Yuwei Wang, Tianshu Chu, Jiarui Tang, Chutang Luo
```

### Introduction
In this work, we propose a Seq2Seq model by using Pointer Sentinel and pre-training embeddings with external text of PTB,which can effectively transform writing style of the literature the literature A Tale of Two Cities to modern English style.


### Requirements
- Python 2.7
- Tensorflow 1.15.0


### Data
Our  dataset is a collection of sentences of the literature A Tale of Two Cities from the  educational site [Sparknotes](www.saparknotes.com). The source provides two versions of the text: the original literature written by Charles Dickens, and a plain translation with modern, easy-to-understand English.  


### Preprocessing: 
 We clean the data by removing blanks at end of paragraphs, deleting empty lines etc. We split the paragraphs into sentences, then filter paragraphs with different number of sentences in two versions of the text as well as sentence that exceeds certain length. To check complete text after initial cleaning, click: [original](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/original_all_cleaned.txt) [modern](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/modern_all_cleaned.txt)


### Instructions to run:
#### Baseline model - Simple Seq2Seq: 
- First run pre-processing
- Change working directory to code/main/
- Run: </br>
`python mt_main.py train 10 seq2seq` </br>
For inference: </br>
- Change working directory to code/main/
- Run: </br>
`python mt_main.py inference tmp/seq2seq5.ckpt greedy` </br>

#### Pointer model: 
- First run pre-processing
- Change working directory to code/main/
- `python mt_main.py train 10 pointer_model` </br>
For inference: </br>
- Change working directory to code/main/
- `python mt_main.py inference tmp/pointer_model7.ckpt greedy` </br>


#### Pre-trained embeddings from PTB text:


#### Pre-trained embeddings using GloVe:




### Reference
Most codes were imported and given credit to the work "Jhamtani H., Gangal V., Hovy E. and Nyberg E. Shakespearizing Modern Language Using Copy-Enriched Sequence to Sequence Models" Workshop on Stylistic Variation, EMNLP 2017

Link to original repository:[click here](https://github.com/harsh19/Shakespearizing-Modern-English)

'''
@article{jhamtani2017shakespearizing,
  title={Shakespearizing Modern Language Using Copy-Enriched Sequence-to-Sequence Models},
  author={Jhamtani, Harsh and Gangal, Varun and Hovy, Eduard and Nyberg, Eric},
  journal={EMNLP 2017},
  volume={6},
  pages={10},
  year={2017}
}
'''
