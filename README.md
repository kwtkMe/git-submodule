# git-submodule

## reference
- [git submodule は癖がすごいとの噂だったが素直につきあっていけそうという話](https://www.d-wood.com/blog/2014/05/22_6257.html)
- [Git submoduleの押さえておきたい理解ポイントのまとめ](https://qiita.com/kinpira/items/3309eb2e5a9a422199e9)
- [Git submodule の基礎](https://qiita.com/sotarok/items/0d525e568a6088f6f6bb)
- [GitHubで複数のリポジトリをネストさせる](https://qiita.com/Statham/items/43da57e6174324d2c68a)

## 概要
### 利点など


### サブモジュールという概念
ざっくり下記
- 親リポジトリに対してネストするリポジトリのこと
- サブモジュールはそれ自体がgitで管理されている
- 親リポジトリにとってサブモジュールは「参照」である
  - サブモジュールのコミットを参照する
  - サブモジュールにコミットなど変更があると親リポジトリが検知する
- サブモジュールの内側は、基本的には親リポジトリ(自分)が操作したときにしか更新されない

### 学習時(?)に留意しておくと良いこと
仕組みを理解するうえで重要なのが以下の点
- 親リポジトリにとってのサブモジュールは(親と)別リポジトリのコミットである
- 現在のサブモジュールのコミット

## 演習
### まずはいろいろ整える
やること
- 親リポジトリにサブモジュールとして他のリポジトリを登録する
  - `git add submodule`
  - `git commit`

### サブモジュールを更新する
下記のような注意点がある
- 親リポジトリ(submodule の外側)と submodule の中が連動しない
  - `git submodule update`という概念
  - 親リポジトリでブランチやコミットの移動をしてもサブモジュールが更新されず、diffが生じる

### (親から見たときの)サブモジュールの状態
`git pull`とか`git status`したときに見慣れない表示が出る
- (new commits)
  - (参照している)サブモジュールが誰かに更新された場合など
  - `git submodule update`をすれば解消する
- (modified content)
  - サブモジュールにdiffがある
    - サブモジュールの中で変更をしたなど
  - `git checkout とか`git add` `git commit`をしてcleanにする
- (modified content)
  - サブモジュールが新しいコミットをしたときなど
  - `git add {submodule}`して`git commit`する
