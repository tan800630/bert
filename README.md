# BERT - forked from google-research

**施工中，未完成**

## 前言

2018年11月釋出的[Bidirectional Encoder Representations from Transformers](https://arxiv.org/abs/1810.04805)論文根基於google前一段時間發表的transformer模型，並且在多個自然語言處理相關作業/比賽上都取得了亮眼的成績。模型架構完全採用transformer-encoder module，而非seq2seq類型的遞迴神經網路(這也是transformer的亮點)，然而在論文中似乎是為了要跟BERT之類的Language Model做一個比較，因此畫的仍然像是序列式處理的模型，一開始我也被搞混了: /


官方也釋出各種版本的pretrain model供使用者下載，以下將我這段時間測試的內容記錄下來。

    註：此版本使用tensorflow框架

## Pretrain Model

已提供之預訓練模型請見[google-research github](https://github.com/google-research/bert)

在以下的範例中，採用[BERT-Base, Multilingual Cased](https://storage.googleapis.com/bert_models/2018_11_23/multi_cased_L-12_H-768_A-12.zip)版本，支援104種語言，總參數量大概在110 Million 左右。

預訓練模型可直接由官方提供的連結下載(.zip檔案)，裏頭包含了模型檔案(bert_model.ckpt)、字典檔案(vocab.txt)、以及模型超參數設定檔(bert_config.json)


## Fine-tune Model with your own data

google團隊提供了GLUE data中幾個資料集的fine-tune方式(在程式碼部分也寫好前處理的部分)，然而若要應用到自己的資料內的話需要自己改寫Processor。

- [bert_IMDB](https://github.com/tan800630/bert-test/blob/master/Python_Scripts/bert_IMDB.ipynb)

在此使用[Imdb sentiment analysis dataset](http://ai.stanford.edu/~amaas/data/sentiment/)作為範例，並稍微修改原始碼，呈現應如何應用此模型到自己的資料中。 (不過這只是單句分類作業，還有另外一塊沒有涵蓋到)  採取的方式是兩階段式的資料整理，首先先將訓練與測試資料儲存為tf_record格式，接著再直接包成input_fn丟入tf.contrib.tpu.TPUEstimator作模型訓練/測試。

    註：由於TFRecordDataset().shuffle運作的方式，發現若資料排序整齊整個模型會訓練不起來。建議在寫入tf_record檔案前手動先shuffle過一遍。

- [bert_IMDB-run_classifier_modified](https://github.com/tan800630/bert-test/blob/master/Python_Scripts/bert_IMDB-run_classifier_modified.ipynb)

同樣使用[Imdb sentiment analysis dataset](http://ai.stanford.edu/~amaas/data/sentiment/)資料，此版本直接修改run_classifier.py中的內容，使其可以應用在Imdb資料集中，修改完的code可在terminal上直接執行訓練與驗證流程。


## Citation

### Imdb 資料來源 
-- <cite>Andrew L. Maas, Raymond E. Daly, Peter T. Pham, Dan Huang, Andrew Y. Ng, and Christopher Potts. (2011). Learning Word Vectors for Sentiment Analysis. The 49th Annual Meeting of the Association for Computational Linguistics (ACL 2011).</cite>