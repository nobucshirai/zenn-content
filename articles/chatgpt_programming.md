---
title: "ChatGPTプログラミングのすすめ"
emoji: "👀"
type: "tech"
topics: ["ChatGPT", "LLM", "Python3", "VSCode"]
published: true
---

ChatGPTなどの大規模言語モデル (Large Language Model; LLM) にプログラミングやリファクタリングをさせる場合、目的に合ったものが作られているかを何らかの方法で検証する必要がある。
プログラムの正しさを完全に保証する方法はないが、ある程度の正しさを継続して担保するための方法を探ってみたので以下にまとめた。
ポイントは、**ChatGPTの生成したプログラムの検証にもやはりChatGPTの力を借りること**である。

## 実行可能性と入出力のチェック

プログラムを生成するタスクである場合、いつでも「実行できるか？」というチェックが可能である。これは自然言語の生成と大きく異なる点だろう。実行可能性を確かめることは最低限のチェック項目になる。
エラーが出力された場合、自力で修正するか、もしくは、エラーの内容をChatGPTに提示して修正を依頼し、再度実行可能かを確かめる。
入力・出力があるプログラムの場合、入力に対して期待した出力が得られるかどうかも確認する。

## プログラム名の提案

ChatGPTにプログラムを作成させたとき、同時にプログラム名も提案させると良い。大抵の場合、気の利いた名前を提案してくれる。プログラム名はそのプログラムの目的や機能を端的に表すものであるため、適切な名前が付けられているかを確認する。

## ヘルプオプションの生成

プログラムにヘルプオプション ( `-h` )を追加することで、ChatGPT自身にそのプログラムの用途や使い方を語らせることができる。このオプションのメッセージが意図したものと一致しているか確認する。
オプションを導入しておくと、機能をオプション単位で追加するようにChatGPTに依頼できるようになる点も利点である。
Pythonであれば `argparse` 、Shellであれば `getopts` の名前をプロンプトに入れておくと成功することが多い。

## README.mdの生成

リポジトリやプログラムを作成した際には、使い方や目的について記述したREADME.mdを用意することが望ましい。しかし、README.mdを作成するのは手間がかかり、プログラムの変更に応じて更新する必要がある。そこで、ChatGPTにREADME.mdの作成と更新をしてもらうと良い。生成・修正されたREADME.mdの内容を読み、自分の意図した動作と一致しているかを確認する。

## VSCodeの編集履歴を確認

Visual Studio Code (VSCode) にはGitとの統合機能があり、最終commitからの変更箇所を簡単に確認できる。この機能を利用することで、プログラムの変更履歴を把握しやすくなる。VSCodeでgit管理されているファイルを開き、編集すると、最終commitからの変更箇所が色付きでハイライトされる。追加された行は緑、削除された行は赤、変更された行は青で表示される。

この機能はChatGPT頼みのリファクタリングや機能追加においても有用である。ChatGPTがどの部分を変更したのかを簡単に確認できるため、生成・修正されたプログラムの理解がしやすくなる。

## Docstringの生成

Docstringは関数・クラスの用途や動作を説明するためのコメントのこと。VSCodeでは、関数・クラスにカーソルを合わせたときに自動的にdocstringの内容がポップアップ表示される機能があり、自作の関数・クラスについてもこの機能が使えて便利である。README.mdと同様にChatGPTに作成してもらうと良い。

## 型ヒントの生成

型ヒント (type hint) は、関数の引数や戻り値の型を明示的に指定するためのもの。Pythonでは3.5以降で使用可能。プログラムの可読性を向上させ、エラーを未然に防ぐために有用なのでChatGPTに頼んで書いてもらうと良い。

## テストプログラムの生成

ChatGPTにプログラムを作成させたとき、同時にそのプログラムのテストプログラムもChatGPTに作成させると良い。テストプログラムがあれば、そのプログラムの動作について別の観点から理解・確認できる上、さらなる更新をChatGPTにさせた場合にも、テストプログラムが通るかどうかでChatGPTの変更が正しいかどうかを確認できる。ChatGPTの生成の不確実さをある程度補完できるため、プログラムの品質向上につながる。
この「ChatGPTが作ったものをChatGPTが作ったもので検証する」という構図は面白いと思う。

## プロンプト例

最後に、上記の複数の項目の要素を含んだプロンプト例を示す。下記のプロンプトを作りたいプログラムの内容の後に追記する形で使用する。

### 仕様追加プロンプト (日本語)

~~~
以下にいくつかの仕様を追加します。
- argparseを使ったヘルプオプションを追加
- docstringsとtype hintsを追加
- スクリプトのファイル名の候補をいくつか提案
- 既存のファイルを上書きする前に"(y)es/(n)o "と尋ねる（デフォルト：no）
- 以下のshebangを追加
```
#!/usr/bin/env python3
```
また、生成したコードの各関数のテストコードを pytest を使って生成してください。
~~~

上記の仕様追加プロンプトの使用例は以下のGitHubページで作成されたPythonスクリプトとともに公開している。

- [PDF_画像結合_Python_2024_0610.md](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/jp_files/PDF_%E7%94%BB%E5%83%8F%E7%B5%90%E5%90%88_Python_2024_0610.md)
- [image_to_pdf_combiner.py](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/jp_files/image_to_pdf_combiner.py)
- [test_image_to_pdf_combiner.py](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/jp_files/test_image_to_pdf_combiner.py)

### 仕様追加プロンプト (英語)

~~~
I would like to add some additional specifications below.
- Add a help option using `argparse`.
- Add docstrings and type hints.
- Suggest some potential filenames for the script.
- Ask "(y)es/(n)o" before overwriting an existing file (default: no). 
- Add the following shebang.
```
#!/usr/bin/env python3
```
Also, please generate a test code for each function of the generated code using pytest.
~~~

英語の仕様追加プロンプトの使用例は以下のGitHubページで作成されたPythonスクリプトとともに公開している。

- [Merge_Images_to_PDF_2024_0609.md](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/Merge_Images_to_PDF_2024_0609.md)
- [merge_images.py](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/merge_images.py)
- [test_merge_images.py](https://github.com/gptdialogues/codegen-showcase/blob/main/1_merge_images/test_merge_images.py)
