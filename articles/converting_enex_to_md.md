---
title: "EvernoteのノートをMarkdownファイルに変換する手順"
emoji: "📓"
type: "tech"
topics: ["Evernote", "Joplin", "Markdown"]
published: true
---

Apr 1, 2024

1. Evernoteのノートをノートブック単位でenex形式でエクスポート
    - ノートブックを右クリックし `Export Notebook`
    - `ENEX format (.enex)` を選んで `Export`
1. Joplinでenexをインポート
    - メニューバー > Import > ```ENEX - Evernote Export File (as Markdown)```
1. Joplinでエクスポート
    - ノートブックを選んで右クリック > Export > ```MD - Markdown + Front Matter```
    - 注意点:
        - 同一ディレクトリに複数のMarkdownファイルを出力すると画像ファイル等が同じ `_resources` ディレクトリに出力されてしまい、後で分離しづらくなってしまう
        - ノートブックごとにディレクトリを作成してエクスポートすることを推奨
1. VSCodeで閲覧・編集
    - Markdownのプレビュー表示のショートカット
        - [macOS] ⌘ + k → v
        - [Windows] (Ctrl) + k → v
