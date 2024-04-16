---
title: Chapter 2 UNIX Commands
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.9
classes: wide
---

[```popular-names.txt```](https://nlp100.github.io/data/popular-names.txt) は, 日本の最高気温の記録を「都道府県」「地点」「℃」「日」のタブ区切り形式で格納したファイルである. 以下の処理を行うプログラムを作成し. [```popular-names.txt```](https://nlp100.github.io/data/popular-names.txt) を入力ファイルとして実行せよ. さらに, 同様の処理を UNIX コマンドでも実行し, プログラムの実行結果を確認せよ.

## 10. 行数のカウント

行数をカウントせよ. 確認には ```wc``` コマンドを用いよ.

```shell
>>> wc -l popular-names.txt
      2780 popular-names.txt
```

## 11. タブをスペースに置換

タブ1文字につきスペース1文字に置換せよ. 確認には ```sed``` コマンド, ```tr``` コマンド, もしくは ```expand``` コマンドを用いよ.

```shell
>>>  sed -e "s/\t/ /g" popular-names.txt
Mary F 7065 1880
Anna F 2604 1880
Emma F 2003 1880
Elizabeth F 1939 1880
Minnie F 1746 1880
Margaret F 1578 1880
Ida F 1472 1880
Alice F 1414 1880
Bertha F 1320 1880
Sarah F 1288 1880
...
```

```shell
>>> tr "\t" " " 0< popular-names.txt
Mary F 7065 1880
Anna F 2604 1880
Emma F 2003 1880
Elizabeth F 1939 1880
Minnie F 1746 1880
Margaret F 1578 1880
Ida F 1472 1880
Alice F 1414 1880
Bertha F 1320 1880
Sarah F 1288 1880
...
```

## 12. 1列目を ```col1.txt``` に，2列目を ```col2.txt``` に保存

各行の1列目だけを抜き出したものを ```col1.txt``` に, 2列目だけを抜き出したものを ```col2.txt``` としてファイルに保存せよ. 確認には ```cut``` コマンドを用いよ.

```shell
for i in 1 2; do cut -f $i popular-names.txt 1> col$i.txt; done
```

## 13. ```col1.txt``` と ```col2.txt``` をマージ

[```12```](https://stmsy.github.io/nlp-100-exercises-chapter-02/#12-1%E5%88%97%E7%9B%AE%E3%82%92-col1txt-%E3%81%AB2%E5%88%97%E7%9B%AE%E3%82%92-col2txt-%E3%81%AB%E4%BF%9D%E5%AD%98) で作った ```col1.txt``` と ```col2.txt``` を結合し, 元のファイルの1列目と2列目をタブ区切りで並べたテキストファイルを作成せよ. 確認には ```paste``` コマンドを用いよ.

```shell
>>> paste col1.txt col2.txt 1> pasted.txt
```

## 14. 先頭から ```N``` 行を出力

自然数 N をコマンドライン引数などの手段で受け取り, 入力のうち先頭の N 行だけを表示せよ. 確認には ```head``` コマンドを用いよ.

```shell
>>> N=5; head -n $N popular-names.txt
Mary    F       7065    1880
Anna    F       2604    1880
Emma    F       2003    1880
Elizabeth       F       1939    1880
Minnie  F       1746    1880
```

## 15. 末尾の ```N``` 行を出力

自然数 N をコマンドライン引数などの手段で受け取り, 入力のうち末尾の N 行だけを表示せよ. 確認には ```tail``` コマンドを用いよ.

```shell
>>> N=5; tail -n $N popular-names.txt
Benjamin        M       13381   2018
Elijah  M       12886   2018
Lucas   M       12585   2018
Mason   M       12435   2018
Logan   M       12352   2018
```

## 16. ファイルを N 分割する

自然数 N をコマンドライン引数などの手段で受け取り, 入力のファイルを行単位で N 分割せよ. 同様の処理を ```split``` コマンドで実現せよ.

```shell
>>> N=5; split -l $N popular-names.txt
```

## 17. 1列目の文字列の異なり

1列目の文字列の種類（異なる文字列の集合）を求めよ. 確認には ```sort```, ```uniq``` コマンドを用いよ.

```shell
>>> sort col1.txt | uniq
Abigail
Aiden
Alexander
Alexis
Alice
Amanda
Amelia
Amy
Andrew
Angela
...
```

## 18. 各行を3コラム目の数値の降順にソート

各行を3コラム目の数値の逆順で整列せよ（注意: 各行の内容は変更せずに並び替えよ）. 確認には ```sort``` コマンドを用いよ（この問題はコマンドで実行した時の結果と合わなくてもよい）.

```shell
>>> sort -k 3rn -t $'\t' popular-names.txt
Linda   F       99689   1947
Linda   F       96211   1948
James   M       94757   1947
Michael M       92704   1957
Robert  M       91640   1947
Linda   F       91016   1949
Michael M       90656   1956
Michael M       90517   1958
James   M       88584   1948
Michael M       88528   1954
...
```

## 19. 各行の1コラム目の文字列の出現頻度を求め，出現頻度の高い順に並べる

各行の1列目の文字列の出現頻度を求め, その高い順に並べて表示せよ. 確認には ```cut```, ```uniq```, ```sort``` コマンドを用いよ.

```shell
>>> cut -f 1 popular-names.txt | sort | uniq -c | sort -rn
 118 James
 111 William
 108 Robert
 108 John
  92 Mary
  75 Charles
  74 Michael
  73 Elizabeth
  70 Joseph
  60 Margaret
...
```

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
