# Parameter and architecture search pattern

## Usecase
- 機械学習モデルの学習前にモデルの最適なハイパーパラメータやアーキテクチャを自動探索したいとき
- 手動でモデル設計やハイパーパラメータ調整をすることが難しいとき

## Architecture
パラメータ＆アーキテクチャ探索パターンは機械学習モデルのハイパーパラメータやアーキテクチャを自動探索するワークフローです。データセットと評価関数に応じたハイパーパラメータやアーキテクチャを自動的に探索することにより、手動でのモデル開発を行う工数を省力化することが可能になります。ハイパーパラメータは学習プロセスを管理する値（分類木の深さやニューラルネットワークの活性化関数等）、アーキテクチャはモデルの全体像（ニューラルネットワークの構造等）を言います。ハイパーパラメータ探索で有名な手法としては、グリッド・サーチ、ランダム・サーチ、遺伝アルゴリズム、ベイズ最適化があります。アーキテクチャ探索では、主にニューラルネットワークの探索手法として、強化学習によるニューラル・アーキテクチャ・サーチや微分によるニューラル・アーキテクチャ・サーチがあります。いずれにおいても、最適な機械学習モデルを自動的に探索する手法になります。<br>
パラメータ＆アーキテクチャ探索パターンは、ハイパーパラメータ探索やアーキテクチャ探索を学習プロセスに組み込むことを目的としています。ワークフローに組み込み、バッチ・ジョブ等で起動できるようにすることで、機械学習モデルの最適化と学習を統合する狙いです。この場合、ハイパーパラメータ探索アルゴリズムやアーキテクチャ探索アルゴリズムおよび、それらの設定値を用意する必要があります。学習用データの取得後、パラメータ＆アーキテクチャ探索ジョブにデータを入力します。パラメータ＆アーキテクチャ探索ジョブでは、探索設定値に応じてモデル探索を行い、学習、評価を実行します。評価結果に応じて次のパラメータやアーキテクチャを決定し、再度学習と評価を実行します。探索→学習→評価のループは、ループ回数や探索対象候補数、時間、評価目標値等で完了します。生成されたモデルは、最後に最適なものをモデル管理システムに記録します。<br>
問題空間に対するベストプラクティスがすでに確立している、または転移学習や再学習で良いモデルを作ることができる場合、本パターンは不向きです。新たなモデル探索や最適化が必要な際に有効なパターンになります。

## Diagram
![diagram](diagram.png)


## Pros
- 機械学習モデルを自動的にチューニングすることで、省力化を図ることが可能。
- 手動では発見できないアーキテクチャを生成する可能性もある。

## Cons
- 探索の設定値を用意する必要がある。
- 探索中の計算リソースにコストが発生する。

## Needs consideration
- パラメータ探索か、アーキテクチャ探索か
- パラメータ探索アルゴリズムまたはアーキテクチャ探索アルゴリズムの選定
- 各探索アルゴリズムの設定値
- コスト対効果