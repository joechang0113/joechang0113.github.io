---
title: Multi-View Vehicle Re-Identiﬁcation using Temporal Attention Model and Metadata Re-ranking
---

## Center Loss

我們常常用softmax loss來求損失，關於softmax loss你可以參考這篇博文：softmax，softmax-loss，BP的解釋。如果你的損失採用softmax loss，那麼最後各個類別學出來的特徵分佈大概如下圖Fig2。這個圖是以MNISTt資料集做的實驗，一共10個類別，用不同的顏色表示。從Fig2可以看出不管是訓練資料集還是測試資料集，都能看出比較清晰的類別界限。

![Image](https://i.imgur.com/GsULP9m.png)

如果你是採用softmax loss加上本文提出的center loss的損失，那麼最後各個類別的特徵分佈大概如下圖Fig3。和Fig2相比，類間距離變大了，類內距離減少了（主要變化在於類內距離：intra-class），這就是直觀的結果。

![Image](https://i.imgur.com/vPGF5Ow.png)