# 課題1

## データセットの作成

### 1.入力データの標準化
輝度は0 ~ 255の256段階で表されている。今回はデータとして扱いやすい形にするため、最大値である255で割ることにより0 ~ 1の間に丸めた。
### 2.データの分割
最初にtensor-flowによりデータセットを読み込み、6:1に分割されている。これらをscikit-learnを用いることにより訓練データ、検証用データ、テストデータを6:0.5:0.5=12:1:1に分割した。

## モデル構築
![model](https://github.com/Jumpei-Fujita/kadai1/blob/master/dentsu_cnn.png)<br>
今回は畳み込みニューラルネットワークにより学習を行い予測を行った。
出力層の活性化関数はReLU関数ではなくSoftplus関数を用いた。<br>
Softplus関数は、微分不可能な点存在しないため、誤差逆伝播がうまく効くと考えられる。
アーキテクチャの概略は以下の通りである。
出力と訓練データのラベルの交差エントロピー誤差を最小にするように学習パラメータの更新を行った。
最適化手法はAdamを選択し、ハイパーパラメータとしてlearning rate,dropout,チャンネル数、カーネルサイズなどの設定を訓練データ、検証用データの評価を考慮して行った。

## テスト結果
### 1.テスト用データに対するPrecision, Recall, F-score
|label|0|1|2|3|4|5|6|7|8|9|
|:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
|Precision|0.96|0.99|0.96|0.99|0.96|0.96|0.99|0.98|0.97|0.98|
|Recall|0.81|0.82|0.83|0.80|0.80|0.80|0.78|0.80|0.79|0.79|
|F-score|0.88|0.90|0.89|0.88|0.87|0.87|0.87|0.88|0.87|0.88|

### 学習の様子
![model](https://github.com/Jumpei-Fujita/kadai1/blob/master/graph_loss.png)
### 検証用データに対する正解率の推移
![model](https://github.com/Jumpei-Fujita/kadai1/blob/master/graph.png)

## コードの実行手順
mnist.ipynbを上から順に実行していく


