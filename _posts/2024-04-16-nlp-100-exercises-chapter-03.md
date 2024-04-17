---
title: Chapter 3 Regular Expressions
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.12
classes: wide
---

Wikipedia の記事を以下のフォーマットで書き出したファイル [jawiki-country.json.gz](https://www.cl.ecei.tohoku.ac.jp/nlp100/data/jawiki-country.json.gz) がある．

- 1行に1記事の情報が JSON 形式で格納される
- 各行には記事名が "title" キーに，記事本文が "text" キーの辞書オブジェクトに格納され，そのオブジェクトが JSON 形式で書き出される
- ファイル全体は `gzip` で圧縮される

以下の処理を行うプログラムを作成せよ．

## 20. JSONデータの読み込み
Wikipedia 記事の JSON ファイルを読み込み，「イギリス」に関する記事本文を表示せよ．問題21-29 では，ここで抽出した記事本文に対して実行せよ．

## 21. カテゴリ名を含む行を抽出
記事中でカテゴリ名を宣言している行を抽出せよ．

## 22. カテゴリ名の抽出
記事のカテゴリ名を（行単位ではなく名前で）抽出せよ．

## 23. セクション構造
記事中に含まれるセクション名とそのレベル（例えば "== セクション名 ==" なら1）を表示せよ．

## 24. ファイル参照の抽出
記事から参照されているメディアファイルをすべて抜き出せ．

## 25. テンプレートの抽出
記事中に含まれる「基礎情報」テンプレートのフィールド名と値を抽出し，辞書オブジェクトとして格納せよ．

## 26. 強調マークアップの除去
[25](https://stmsy.github.io/nlp-100-exercises-chapter-03/#25-%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%81%AE%E6%8A%BD%E5%87%BA) の処理時に，テンプレートの値からMediaWikiの強調マークアップ（弱い強調，強調，強い強調のすべて）を除去してテキストに変換せよ（参考: [マークアップ早見表](http://ja.wikipedia.org/wiki/Help:%E6%97%A9%E8%A6%8B%E8%A1%A8)）．

## 27. 内部リンクの除去
[26](https://stmsy.github.io/nlp-100-exercises-chapter-03/#26-%E5%BC%B7%E8%AA%BF%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E9%99%A4%E5%8E%BB) の処理に加えて，テンプレートの値から MediaWiki の内部リンクマークアップを除去し，テキストに変換せよ（参考: [マークアップ早見表](http://ja.wikipedia.org/wiki/Help:%E6%97%A9%E8%A6%8B%E8%A1%A8)）．

## 28. MediaWikiマークアップの除去
[27](https://stmsy.github.io/nlp-100-exercises-chapter-03/#28-mediawiki%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E9%99%A4%E5%8E%BB) の処理に加えて，テンプレートの値から MediaWiki マークアップを可能な限り除去し，国の基本情報を整形せよ．

## 29. 国旗画像のURLを取得する
テンプレートの内容を利用し，国旗画像の URL を取得せよ．（ヒント: [MediaWiki API](http://www.mediawiki.org/wiki/API:Main_page/ja) の [imageinfo](http://www.mediawiki.org/wiki/API:Properties/ja#imageinfo_.2F_ii) を呼び出して，ファイル参照を URL に変換すればよい）

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
