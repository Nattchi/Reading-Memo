# 実践データ活用システム開発ガイド

![実践データ活用システム開発ガイド](https://hondana-image.s3.amazonaws.com/book/image/616180/53b1bba1-2711-40a6-b755-b1e9ef822921.jpg)

# 1. コンセプトサマリー

## はじめに

### 1.1.1 データ活用基盤とは何か

![データ活用基盤](https://data-viz-lab.com/wp-content/uploads/2020/03/1.png)

### 1.1.2 データ活用の流れ

分散処理

- スケールアップ：サーバーの性能を上げる
- スケールアウト：サーバーの台数を増やす

POC（Proof of Concept）：概念実証

- ABテスト：AとBのどちらが良いかを検証する
- MVP（Minimum Viable Product）：最小限の機能を持った製品を作る

### コラム1.1 機械学習による”モデル”の困難

機会学習モデルの登場により，通常のシステム開発とは異なる困難に見舞われるようになった．ブラックボックステストの困難，精度が変化・劣化するという困難である．
ECサイトを例にとると，ユーザーの購買行動を予測するモデルを作成したとする．
過去の購入履歴が学習データ，ユーザーIDが入力データ，レコメンドする商品が出力データとなる．
機械学習モデルは季節や直近のユーザーの嗜好の変化を学習することにより，最適な出力が得られるメリットがあるが，挙動がブラックボックスしやすいデメリットがある．
ユーザーの嗜好の変化に対応するためには，常に新しい学習データによる学習が必要となる．

データ活用基盤に以下の要件が求められるようになってきた．

1. 機械学習モデルの容易なテスト
1. 機械学習モデルの劣化を防ぐように再学習できること
1. 機械学習モデルがどのぐらい劣化しているのか，可視化できること

### 1.1.3 データ活用基盤開発の困難さ

#### データ活用基盤開発者が抱える課題

- データ活用基盤開発における機能要件・非機能要件がわからない
- あれもこれも機能追加を試みて，開発工数が膨らむ
- 複雑なデータ活用基盤となり，運用が困難になる
- 開発中に要件や開発環境が変化し，開発が難航する

#### データ活用基盤利用者が抱える課題

- 複雑なデータ活用基盤を使いこなせない
- 欲しい機能と提供されている機能がマッチしていない

## 1.2 本書のアプローチ

前節で挙げた課題を解決するために，本書では`MVP`と`ロードマップ`を作成するアプローチを取る．

### 1.2.1 MVPとは

MVP(Minimum Viable Product)とは，最小限の機能を持った製品のことである．

[MVPの意味を理解する](https://www.ankr.design/designtips/making-sense-of-mvp)

### 1.2.2 ロードマップとは

ロードマップ：MVPを作成する際に，大まかな方向性やゴール，開発時期を可視化するものである．

## 1.3 スターターキットとは

# 2. データの収集と蓄積

## 2.1 データ活用の第一歩
