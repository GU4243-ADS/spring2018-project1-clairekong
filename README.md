---
title: "Who wrote the scariest novels/poems"
Author: "Mingyue Kong"
output:
  html_document:
    df_print: paged
    toc: yes
    keep_md: yes
  pdf_document:
    toc: yes
---
# Introduction

In this exploratory analysis, the work of three masters of horror novel/poem will be examined. The analysis tries to find out who wrote the scariest novels/poems. Three authors, namely Edgar Allan Poe, Mary Wollstonecraft Shelley and Howard Phillips Lovecraft???are popular horror authors in their time and in their countries. 

![Let's get started](/Users/Clairiakong/Desktop/Spooky.PNG)

This analysis is mainly based on sentiment analysis and is divided into 2 major sections: single unit (word) analysis and full unit (paragraph) analysis. Packages used in this analysis include ggplot2, tibble, tidyr, stringr, tidytext, wordcloud, ggridges, dplyr, stopwords, sentimentr and tidyverse. 



# Single Unit Analysis
## Seperating dataset

The dataset (spooky.csv) contains texts from works written by spooky authors: Edgar Allan Poe, Howard Phillips Lovecraft and Mary Wollstonecraft Shelley. The dataset has three columns: id, text and author. First, let's explore the data. 

```
##    Length     Class      Mode 
##     19579 character character
```
We could see that, among 19579 rows, 7900 texts belong to EAP (Edgar Allan Poe), 5635 texts belong to HPL (Howard Phillips Lovecraft) and 6044 texts belong to MWS (Mary Wollstonecraft Shelley). 

To further analyse each word in given texts, I separated the dataset by authors' names and built up three datasets for each author. 

```
##       id                text           author    
##  Length:7900        Length:7900        EAP:7900  
##  Class :character   Class :character   HPL:   0  
##  Mode  :character   Mode  :character   MWS:   0
```

```
##       id                text           author    
##  Length:5635        Length:5635        EAP:   0  
##  Class :character   Class :character   HPL:5635  
##  Mode  :character   Mode  :character   MWS:   0
```

```
##       id                text           author    
##  Length:6044        Length:6044        EAP:   0  
##  Class :character   Class :character   HPL:   0  
##  Mode  :character   Mode  :character   MWS:6044
```
## Cleaning data

Then, I cleaned the data by removing all punctuation and transform all words into lower case using unnest_tokens and removing stopwords using anti_join. 



![Tidy Data Example](/Users/Clairiakong/Desktop/tidyeap.PNG)

## Word frequency - Word Cloud
Now I will look into what are the most frequent words in each author's works by visualizing the data with word cloud function. Comparing the most frequent 100 words in each author's works, we may have a general idea of whose work is the scariest one. 

```
## [1] 729 563 559 559 540 516
```

![](Who_wrote_the_scariest_novels_poems_files/figure-html/Word Cloud-1.png)<!-- -->

```
## [1] 260 230 178 174 168 164
```

![](Who_wrote_the_scariest_novels_poems_files/figure-html/Word Cloud-2.png)<!-- -->

```
## [1] 254 238 188 186 174 169
```

![](Who_wrote_the_scariest_novels_poems_files/figure-html/Word Cloud-3.png)<!-- -->

```
## [1] 329 273 262 248 243 231
```

![](Who_wrote_the_scariest_novels_poems_files/figure-html/Word Cloud-4.png)<!-- -->

The above word clouds for three authors show the most frequent 100 words in their works. We could see that in EAP used words such as time and length most frequently in his work, HPL used words such as night, strange and heard most frequently in his work while MWS used words such as raymond, love and life most frequently in her work (which do not seem scary to me).

## Sentiment Analysis - word level

In this section, I apply sentiment analysis using NRC sentiment lexion. "The NRC Emotion Lexicon is a list of English words and their associations with eight basic emotions (anger, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments (negative and positive). The annotations were manually done by crowdsourcing." 



![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-2-1.png)<!-- -->




![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-4-1.png)<!-- -->




![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

Looking at the word-level sentiment analysis of three authors, we notice that HPL used fear and negative words most frequently while MWS and EAP used more positive words. 

## Words that make you fear

To further look into whose work is the scariest one, I filter the sentiment "fear" in the NRC lexicon and sorted the fear words that three authors used in their works to compare. 



![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
Surprisingly, MWS used words such as death and fear more often than other two authors while she also used expressed more positive feelings in her works than others did. 

# Full Unit Analysis

Based on above analysis, it is still hard to say that who is the scariest author. Therefore, it may be necessary to look at different units of text and try to understand the sentiment of a sentence or paragraph as a whole. I cleaned the original dataset by removing all punctuation and transform all words into lower case using unnest_tokens and removing stopwords using anti_join and kept sentences in the original dataset instead of separating them into words. 



![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-10-1.png)<!-- -->![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

I made two plots to compare authors' usage of fear words on the sentence level. As Plot 1 and Plot 2 show, HPL's works is the scariest for most of sentences in his works express fear or negative feelings while the works of EAP and MWS both tend to express more positive sentiment than HPL did. 

![](Who_wrote_the_scariest_novels_poems_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

Last, I tried to "score" each author's works with Bing sentiment lexion which categorizes words in a binary fashion into positive and negative categories. As the result show, MWS tends to be the least scaries author and HPL tends to be the scaries author for his works score -5 on average. One sentence of EAP's works scores -10; however, his works are not as scary as HPL's on average. 
