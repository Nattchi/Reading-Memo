# コンパイラ：ガベージコレクション

## 7.5 ごみ集めの基礎

- オブジェクトの到達可能性(7.5.2)

- 参照カウントを用いたGC(不完全ではあるが)(7.5.3)

- トレース方式のGC(7.6)

### 7.5.1 ごみ集めの設計目標

定義：アクセス不能になったオブジェクトが使用していた記憶領域を再利用すること

GCは実行時にオブジェクトの型がわかると仮定する．

1つのオブジェクトへの参照は同じ値を持つ

ミューテータ：ヒープ中に存在するオブジェクトの書き換えを行うプログラム

ミューテーション：メモリ管理ルーチンからメモリ空間を獲得し，新たなオブジェクトの生成や既存オブジェクトの参照の生成，削除などの操作

#### 型安全性

型安全：どんなデータ成分についても，型が言語で決定できる

静的型付き言語(コンパイル時)→動的型付き言語(実行時)→不完全な言語

※プログラミング言語との比較表があるとよさそう

#### 性能の評価尺度

GCは非常にコストが高い，性能について考える際の評価尺度を紹介する

- 全実行時間

GCでは大量のデータを調べる必要がある．メモリサブシステムをどれくらい有効活用できるかが，性能に直結する

- 空間使用効率

メモリ空間の断片化を防ぎ，使用可能な領域を最大限利用できるようにする

- 中断時間

領域の回収を行った場合，プログラムの実行が突然，長い間にわたって中断させてしまう．
限られた時間内に実行しなければならない処理との相性が特に悪い

- ごみ集めを控えるか

- 中断時間の最大値を制限する

といった対応が必要となる．

- プログラム局所性

ミューテーターのメモリ空間的局所性を改善

### 7.5.2 到達可能性

ルート集合：プログラムで直接アクセスができるデータ
※ポインタを通して参照されるデータは除く

    EX. Java
    静的フィールドメンバとスタック上のすべての変数

到達可能性：

到達可能なオブジェクトのフィールドメンバや配列要素内に格納されている参照により，参照可能となるオブジェクトも到達可能

プログラムにコンパイラによる最適化がかかる場合：
