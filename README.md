# README
#### スライド
- slide.pdf, slide.pptx  
  研究発表のためのスライド

#### 前処理
- mkMFCC.py  
  audioをMFCCに変換する
- mkFT.py  
  audioを短時間フーリエ変換する
- mp3towav.py  
  mp3ファイルをwavファイルに変換する
- loadWav.py  
  wavファイルを読み込みcsvファイルに変換・保存する
  wavファイルを読み込みモデルの入力に変換する
- loadCsv.py  
  csvファイルを読み込みモデルの入力に変換する
- readFav.py  
  楽曲に割り当てた好きな部分をラベルとして教師信号を作成する


#### モデル
- my2dCNN+LSTM.py  
  モデル
- prediction2d+LSTM.py  
  学習したモデルを使って予測結果を出力する

### 研究概要
深層学習を利用した音楽推薦システムの提案．  
深層学習を利用することでユーザの好みを学習し楽曲を推薦する．入力は楽曲をaudioをメル周波数ケプストラム係数に変換したもの．教師信号は楽曲の楽曲内のある8秒間に割り当てられた好きかそうでないかの0, 1の値を教師信号としている．

学習
1. audio形式の楽曲をMFCCに変換し入力データを作成
2. 変換した楽曲を8秒ごとに短く切る
3. CNNで時間領域のみを畳み込み楽曲の特徴量を抽出
4. CNNによって抽出した特徴量をLSTMに入力し、LSTMによって好みの程度を出力
5. 出力値と教師データを比較してCNN・LSTMの重みを学習
これを繰り返すことで学習する．

予測
1. audio形式の楽曲をMFCCに変換し入力データを作成  
2. 8秒の間隔の窓を1秒ずつずらし変換した楽曲を短く切る
3. CNNに②を入力
4. CNNの出力値をLSTMに入力
5. 入力された8秒ごとの楽曲にどれくらい好きなのかを出力
6. 8秒ごとの出力を足し合わせ，楽曲の時間で割った値を比較し一番値の高い楽曲を推薦
