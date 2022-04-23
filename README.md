# 株式会社ゆめみ Android エンジニアコードチェック課題

## 概要

本プロジェクトは株式会社ゆめみ（以下弊社）が、弊社に Android エンジニアを希望する方に出す課題のベースプロジェクトです。本課題が与えられた方は、下記の概要を詳しく読んだ上で課題を取り組んでください。

## アプリ仕様

本アプリは GitHub のリポジトリを検索するアプリです。

<img src="docs/app.gif" width="320">

### 環境

- IDE：Android Studio Arctic Fox | 2020.3.1 Patch 1
- Kotlin：1.5.31
- Java：11
- Gradle：7.0.1
- minSdk：23
- targetSdk：31

※ ライブラリの利用はオープンソースのものに限ります。

### 動作

1. 何かしらのキーワードを入力
2. GitHub API（`search/repositories`）でリポジトリを検索し、結果一覧を概要（リポジトリ名）で表示
3. 特定の結果を選択したら、該当リポジトリの詳細（リポジトリ名、オーナーアイコン、プロジェクト言語、Star 数、Watcher 数、Fork 数、Issue 数）を表示

## 開発方法
1. issue ごとに feature branch を切り，作業はそこで行う．
2. 一段落するごとに commit し，一連の作業が終わったら動作確認の後 dev branch に pull request を行う．
3. 問題なければ merge し，それぞれの branch に dev から pull を行う．
4. 修正が完了したら dev branch から main branch に pull request を行う． 
5. 問題がなければ merge する．

## やったこと
- ### issue1
  - 命名規約に基づくObjectの名称変更
  - coding conventionに基づくReformat (改行位置，空白etc)
  - comment 追加
  - typo 修正 
- ### issue2
  - 非null表明演算子の削除とその対応
  - `lateinit` 削除とその対応
- ### issue3
  - layout の修正
  - dark-mode への対応 (文字色変更)
  - LeakCanary 導入 (Memory Leak が検出できる)  

### やってみたけどうまくいかなかったこと
- class item -> Item への名称変更
  - Refactor -> Rename を使用したので，変更すべき箇所の選定がうまくできていなかったか
  - 結局元に戻しitem のまま  
- Memory Leak の解消
  - `TwoFragment.kt`(https://github.com/WMs784/yumemi_code-check/blob/main/app/src/main/kotlin/jp/co/yumemi/android/code_check/TwoFragment.kt) に
    `onDestroyView`を追加したが，うまく解消できなかった．
  - Memory Leak についてはよくわかっていなかったので，今回のテストで色々調べて勉強になった．

### できなかったこと
- issue #4 Fat Fragment の解消
  - Fat Fragment は聞いたことがない言葉だったので色々と調べたが，参考になりそうなものをうまく見つけることができなかった．
  - Fragmentの複数のFragmentに分ければ良いということなのかなと思ったが，やり方わからず．
- null に対する例外処理
  - 検索結果がない場合に「検索結果はありません」みたいな表示が作れたらよかった．
  - Repository 詳細画面でも取得した data (ex.language)がnull だった場合の処理が必要になる.
    