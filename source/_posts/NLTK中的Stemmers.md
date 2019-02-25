---
title: 'NLTK中的Stemmers'
date: 2019-02-23 12:35:08
categories: 
  - Python
tags:
  - Python
  - NLTK
 
---
# Stemmers

在英语中，一个单词常常是另一个单词的“变种”，如：happy=>happiness，这里happy叫做happiness的词干（stem）。在信息检索系统中，我们常常做的一件事，就是在Term规范化过程中，提取词干（stemming），即除去英文单词分词变换形式的结尾。
<!-- more --> 

本文主要介绍nltk中Stemmer的用法

### Porter Stemmer
应用最为广泛的、中等复杂程度的、基于后缀剥离的词干提取算法是波特词干算法，也叫波特词干器（Porter Stemmer）。  

```python
from nltk.stem.porter import *
stemmer = PorterStemmer()
plurals = ['caresses', 'flies', 'dies', 'mules', 'denied','died', 'agreed', 'owned', 'humbled', 'sized','meeting', 'stating', 'siezing', 'itemization','sensational', 'traditional', 'reference', 'colonizer','plotted']
singles = [stemmer.stem(plural) for plural in plurals]
print(' '.join(singles))

'''
output: caress fli die mule deni die agre own humbl size meet
state siez item sensat tradit refer colon plot
'''
```
### Snowball stemmer
雪球词干算法（不知道该怎么翻译=.=）支持多种语言
```python
>>> from nltk.stem.snowball import SnowballStemmer
>>> print(" ".join(SnowballStemmer.languages))
danish dutch english finnish french german hungarian italian
norwegian porter portuguese romanian russian spanish swedish
```
以英语为例：
```python
>>> stemmer = SnowballStemmer("english")
>>> print(stemmer.stem("running"))
run
```
可以设置忽略停用词：
```python
>>> stemmer2 = SnowballStemmer("english", ignore_stopwords=True)
>>> print(stemmer.stem("having"))
have
>>> print(stemmer2.stem("having"))
having
```
一般来说，SnowballStemmer("english")要比PorterStemmer()更准确。
```python
>>> print(SnowballStemmer("english").stem("generously"))
generous
>>> print(SnowballStemmer("porter").stem("generously"))
gener
```

### LancasterStemmer
也是一种词干提取器，直接看代码吧。
```python
>>> from nltk.stem.lancaster import LancasterStemmer
>>> lancaster_stemmer = LancasterStemmer()
>>> lancaster_stemmer.stem(‘maximum’)
‘maxim’
>>> lancaster_stemmer.stem(‘presumably’)
‘presum’
>>> lancaster_stemmer.stem(‘presumably’)
‘presum’
>>> lancaster_stemmer.stem(‘multiply’)
‘multiply’
>>> lancaster_stemmer.stem(‘provision’)
u’provid’
>>> lancaster_stemmer.stem(‘owed’)
‘ow’
```