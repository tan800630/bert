# BERT - forked from google-research

**施工中**

## 前言

2018年11月釋出的[Bidirectional Encoder Representations from Transformers](https://arxiv.org/abs/1810.04805)論文根基於google前一段時間發表的transformer模型，並且在多個自然語言處理相關作業/比賽上都取得了亮眼的成績。官方也釋出各種版本的pretrain model供使用者下載，以下將我這段時間測試的內容記錄下來。

    註：此版本使用tensorflow框架

## Pretrain Model

請見[google-research github](https://github.com/google-research/bert)

## Fine-tune Model with your own data

google團隊提供了GLUE data中幾個資料集的fine-tune方式(在程式碼部分也寫好前處理的部分)，然而若要應用到自己的資料內的話需要自己改寫Processor。

在此使用Imdb sentiment analysis dataset作為範例，並稍微修改原始碼，呈現應如何應用此模型到自己的資料中。 (不過這只是單句分類作業，還有另外一塊沒有涵蓋到)