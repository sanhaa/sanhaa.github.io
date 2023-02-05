---
layout: post
title: NLP | soynlp 라이브러리 소개
description: >
  
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


## soynlp
> 사전 기반이 아니라, 학습 데이터 내 자주 발생하는 패턴을 기반으로 단어의 경계선을 구분

[soynlp 깃허브 바로가기](https://github.com/lovit/soynlp) 

~~~python
from soynlp.utils import DoublespaceLineCorpus
from soynlp.noun import LRNounExtractor_v2
from soynlp.word import WordExtractor

train_data = DoublespaceLineCorpus("train.txt") # 데이터기반 패턴 학습

### 명사 추출
noun_extractor = LRNounExtractor_v2() # extractor 객체 생성
nouns = noun_extractor.train_extract(train_data) # train_data에서 명사 추출

### 단어 추출
word_extractor = WordExtractor() # extractor 객체 생성
words = word_extractor.train_extract(train_data) # train_data에서 단어 추출

~~~

- 학습 데이터를 기반으로 단어를 추출하기 때문에
- 시간이 오래 걸린다.
- 학습 데이터에 따라 단어 추출이 달라질 수 있다.