# Literature Style Transfer


This is code implementation of the final project of DS-GA 1012:
```
Text-style Transformation from 19th-Century Literature to Modern Language
Yuwei Wang, Tianshu Chu, Jiarui Tang, Chutang Luo
```
In addition to collaborators, we would like to sincerely thank our professor [Sam Bowman](https://cims.nyu.edu/~sbowman/) for valuable advice and guidance.

The complete project report can be found [here](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/Final%20Report.pdf)

### Introduction
In this project, we propose a Seq2Seq model by using Pointer Sentinel and pre-training embeddings to effectively transform writing style of the classical literature to plain English. We also introduce a new parellel text set from A Tale of Two Cities by Charles Dickens.


### Requirements
- Python 2.7
- Tensorflow 1.15.0


### Data
Our  dataset is a collection of sentences of the literature A Tale of Two Cities from the  educational site [Sparknotes](www.saparknotes.com). The source provides two versions of the text: the original literature written by Charles Dickens, and a plain translation with modern, easy-to-understand English.  


### Preprocessing: 
 We clean the data by removing blanks at end of paragraphs, deleting empty lines etc. We split the paragraphs into sentences, then filter paragraphs with different number of sentences in two versions of the text as well as sentence that exceeds certain length. 
 - To check complete text after initial cleaning, click: [original](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/original_all_cleaned.txt) [modern](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/modern_all_cleaned.txt)
- To check splited and filtered sentence paris, click: [original](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/two_cities_original_sentence.txt) [modern](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/two_cities_modern_sentence.txt)

### Instructions to run:

#### Pre-processing:
- Change working directory to code/main/
- Create a new directory named 'tmp'
- Run: </br>
`python mt_main.py preprocessing` </br>

*You need to run pre-processing before running any models below*

#### Simple Seq2Seq: 
- In code/main, open configuration.py: </br>
  - Change line 11 to `use_pointer=False`
- run: </br>
`python mt_main.py train 10 seq2seq` </br>
For inference: </br>
- Change working directory to code/main/
- Run: </br>
`python mt_main.py inference tmp/seq2seq5.ckpt greedy` </br>

#### Pointer model: 
- In code/main, open configuration.py: </br>
  - change line 11 to `use_pointer=True`
- run: </br>
- `python mt_main.py train 10 pointer_model` </br>
For inference: </br>
- Change working directory to code/main/
- `python mt_main.py inference tmp/pointer_model7.ckpt greedy` </br>

#### Pre-trained embeddings from PTB text:
- In code/main, open configuration.py: </br>
  - change line 19 to:
   `pretrained_embeddings_path = data_dir + "embeddings/retrofitted_external_192_startend.p"`
- Then use same commands as before for running model and testing

#### Pre-trained embeddings using GloVe:
- Change directory to data/embeddings, follow instruction in [GloVe_Embeddings.ipynb](https://github.com/yuwei-jacque-wang/Literature-Style-Transfer-DSGA1012/blob/master/data/embeddings/GloVe_Embedding.ipynb) to create GloVe embeddings
- Change directory back to code/main, open configuration.py: </br>
  - change line 19 to:
   `pretrained_embeddings_path = data_dir + "embeddings/glove.p"`
- Then use same commands as before for running model and testing

#### Tune hyperparameters:
- In code/main.configuration.py, change the following options:
  - max_input_seq_length & max_output_seq_length
  - max_vocab_size
  - lstm_cell_size & embeddings_dim (need to use new embeddings if you change this option)
  - use_sentinel_loss (for Pointer model)


### Reference
Most codes were imported and given credit to the work "Jhamtani H., Gangal V., Hovy E. and Nyberg E. Shakespearizing Modern Language Using Copy-Enriched Sequence to Sequence Models" Workshop on Stylistic Variation, EMNLP 2017

Link to original repository:[click here](https://github.com/harsh19/Shakespearizing-Modern-English)

```
@article{jhamtani2017shakespearizing,
  title={Shakespearizing Modern Language Using Copy-Enriched Sequence-to-Sequence Models},
  author={Jhamtani, Harsh and Gangal, Varun and Hovy, Eduard and Nyberg, Eric},
  journal={EMNLP 2017},
  volume={6},
  pages={10},
  year={2017}
}
```
