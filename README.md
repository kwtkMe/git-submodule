# git-submodule

## reference
- [git submodule は癖がすごいとの噂だったが素直につきあっていけそうという話](https://www.d-wood.com/blog/2014/05/22_6257.html)
- [Git submodule の基礎](https://qiita.com/sotarok/items/0d525e568a6088f6f6bb)
- [GitHubで複数のリポジトリをネストさせる](https://qiita.com/Statham/items/43da57e6174324d2c68a)

## 概要
### サブモジュールという概念
さっくり下記
- 親リポジトリに対してネストするリポジトリのこと
- サブモジュールはそれ自体がgitで管理されている
- 親リポジトリにとってサブモジュールは「参照」である
  - サブモジュールのコミットを参照する
  - サブモジュールにコミットなど変更があると親リポジトリが検知する
- サブモジュールの内側は、基本的には親リポジトリ(自分)が操作したときにしか更新されない

### 学習時(?)に留意しておくと良いこと
仕組みを理解するうえで重要なのが
- 親リポジトリにとってのサブモジュールは(親と)別リポジトリのコミットである
- 現在のサブモジュールのコミット

### サブモジュールを更新する
下記のような注意点がある
- リポジトリA (submodule の外側) と submodule の中が連動しない
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
