# How to use Git

## Make repository(基礎的な使用法)
- `git init`：ワーキングディレクトリおよびそれ以下の階層が管理対象となる<br>
- `echo`とか`touch`でファイル作成<br>
- `git add [. or 対象となるファイル]`：ファイルをステージングする<br>
- `git commit -m “コメント”`：リモートリポジトリに反映させる
<br><br>
## branchを作る
### そもそもbranchとは
時間軸のことを表す．チームで開発を行う場合，各々でbranchを作成し，その中で作業を行って最後に統合するイメージ．<br>
- `git branch hoge`：hogeという名前のbranchを作成する<br>
- `git branch`：branch一覧の表示<br>
- `git checkout hoge`：hogeに移動<br>
<br><br>
## branchをmergeする
以下のbranchがあるとする．
* hoge
* master<br>

`master`に`hoge`をmergeすることを想定する．
```
git checkout master /* masterへ移動 */
git merge hoge /* hogeをmasterへマージ */
```
<br><br>
## コンフリクトしたら．．．
mergeする/されるファイルの両方でbranchで同箇所に変更を加えると，競合が発生する．(コンフリクト)<br>
この場合，手動で差分を取り込んで解決する必要あり．
- `git status`：コンフリクトしているファイルが特定できる
- `git merge-base <branch_A> <branch_B>`：2つのbranchがどこから分岐しているか特定する(コミットidがわかる)
- `git diff <特定のコミットid> <branch_A> <比較ファイル>`：`特定のコミットidのブランチ`と`branch_A`の`比較ファイル`の内容の比較を行う．<br>

コンフリクト箇所が特定できたら，どちらかに内容を統一した上で，`git merge --continue`で再度マージする．
