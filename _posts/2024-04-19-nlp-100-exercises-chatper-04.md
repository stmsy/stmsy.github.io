---
title: Chapter 4 POS Tagging
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.12
classes: wide
---

夏目漱石の小説『吾輩は猫である』の文章（[`neko.txt`](http://www.cl.ecei.tohoku.ac.jp/nlp100/data/neko.txt)）を MeCab を使って形態素解析し, その結果を neko.txt.mecab というファイルに保存せよ. このファイルを用いて, 以下の問に対応するプログラムを実装せよ.

なお，問題[37](https://stmsy.github.io/nlp-100-exercises-chatper-04/#37-%E9%A0%BB%E5%BA%A6%E4%B8%8A%E4%BD%8D10%E8%AA%9E), [38](https://stmsy.github.io/nlp-100-exercises-chatper-04/#38-%E3%83%92%E3%82%B9%E3%83%88%E3%82%B0%E3%83%A9%E3%83%A0), [39](https://stmsy.github.io/nlp-100-exercises-chatper-04/#39-zipf-%E3%81%AE%E6%B3%95%E5%89%87)は [matplotlib](http://matplotlib.org/) もしくは [Gnuplot](http://www.gnuplot.info/) を用いるとよい.

## 30. 形態素解析結果の読み込み

形態素解析結果（neko.txt.mecab）を読み込むプログラムを実装せよ. ただし, 各形態素は表層形（`surface`）, 基本形（`base`）, 品詞（`pos`）, 品詞細分類1（`pos1`）をキーとするマッピング型に格納し, 1文を形態素（マッピング型）のリストとして表現せよ. 第4章の残りの問題では, ここで作ったプログラムを活用せよ.

## 31. 動詞

動詞の表層形をすべて抽出せよ.

## 32. 動詞の原形

動詞の原形をすべて抽出せよ.

## 33. サ変名詞

サ変接続の名詞をすべて抽出せよ.

## 34. 「AのB」

2つの名詞が「の」で連結されている名詞句を抽出せよ.

## 35. 名詞の連接

名詞の連接（連続して出現する名詞）を最長一致で抽出せよ.

## 36. 単語の出現頻度

文章中に出現する単語とその出現頻度を求め, 出現頻度の高い順に並べよ.

## 37. 頻度上位10語

出現頻度が高い10語とその出現頻度をグラフ（例えば棒グラフなど）で表示せよ.

## 38. ヒストグラム

単語の出現頻度のヒストグラム（横軸に出現頻度, 縦軸に出現頻度をとる単語の種類数を棒グラフで表したもの）を描け.

## 39. Zipf の法則

単語の出現頻度順位を横軸, その出現頻度を縦軸として, 両対数グラフをプロットせよ.

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
