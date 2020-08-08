# 0~9 手書き数字（MNISTデータセット）の分類

## データセットの作成・前処理
・MNISTデータセットは各ピクセルにおいて輝度0 ~ 255の256段階で表されている。データとして扱いやすい形にするため、最大値である255で割ることにより0 ~ 1の間に丸める。
・tensor-flowによりデータセットを読み込み、6:1に分割されている。
・scikit-learnを用いることにより訓練データ、検証用データ、テストデータを 6:0.5:0.5 = 12:1:1に分割した。

## 構築した深層学習モデル
今回は畳み込みニューラルネットワーク（CNN）により学習を行い予測をおこなう。 出力層の活性化関数はReLU関数ではなくSoftplus関数を用いる。
Softplus関数は、微分不可能な点が存在しないため、誤差逆伝播がうまく効くと考えられているからである。実際にReLUとSoftplusを比較したとき、精度に大きな差が生まれた。
アーキテクチャの概略は以下の通りである。 出力データと訓練データのラベルの交差エントロピー誤差を最小にするように学習パラメータの更新を行う。
最適化手法はAdamを選択し、ハイパーパラメータとしてlearning rate,dropout,チャンネル数、カーネルサイズなどの設定を訓練データ、検証用データの評価を考慮して行った。

![mnist_cnn](https://user-images.githubusercontent.com/57475794/89707687-84457180-d9ab-11ea-9531-ac8091a98742.png)

## 結果
![mnist_graph_loss](https://user-images.githubusercontent.com/57475794/89707633-05503900-d9ab-11ea-959b-5515315f55a5.png)

![mnist_acc](https://user-images.githubusercontent.com/57475794/89707663-4cd6c500-d9ab-11ea-9593-74d3337de1dc.png)

