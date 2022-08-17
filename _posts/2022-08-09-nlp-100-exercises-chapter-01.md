---
title: Chapter 1 Warm-up
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.9
classes: wide
---

## 00. 文字列の逆順

文字列 ```"stressed"``` の文字を逆に（末尾から先頭に向かって）並べた文字列を得よ.

```python
>>> word = "stressed"
>>> print(word[::-1])
desserts
```

## 01. 「パタトクカシーー」

```"パタトクカシーー"```という文字列の1, 3, 5, 7文字目を取り出して連結した文字列を得よ.

```python
>>> word = "パタトクカシーー"
>>> print(word[::2])
パトカー
```

## 02. 「パトカー」＋「タクシー」＝「パタトクカシーー」

```"パトカー"```＋```"タクシー"```の文字を先頭から交互に連結して文字列```"パタトクカシーー"```を得よ.

```python
>>> first, second = "パトカー", "タクシー"
>>> concated = ["" for _ in range(len(first + second))]
>>> concated[::2] = list(first)
>>> concated[1::2] = list(second)
>>> word = "".join(concated)
>>> print(word)
パタトクカシーー
```

## 03. 円周率

```"Now I need a drink, alcoholic of course, after the heavy lectures involving quantum mechanics."``` という文を単語に分解し, 各単語の（アルファベットの）文字数を先頭から出現順に並べたリストを作成せよ.

```python
>>> sent = ("Now I need a drink, alcoholic of course, after the heavy lectures "
...         "involving quantum mechanics.")
>>> words = [word.rstrip(',.') for word in sent.split(' ')]
>>> counts = [len(word) for word in words]
>>> print(counts)
[3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5, 8, 9, 7, 9]
```

## 04. 元素記号

```"Hi He Lied Because Boron Could Not Oxidize Fluorine. New Nations Might Also Sign Peace Security Clause. Arthur King Can."``` という文を単語に分解し, 1, 5, 6, 7, 8, 9, 15, 16, 19番目の単語は先頭の1文字, それ以外の単語は先頭に2文字を取り出し, 取り出した文字列から単語の位置（先頭から何番目の単語か）への連想配列（辞書型もしくはマップ型）を作成せよ.

```python
>>> sent = ("Hi He Lied Because Boron Could Not Oxidize Fluorine. "
...         "New Nations Might Also Sign Peace Security Clause. Arthur King Can.")
>>> elems = [word.rstrip(',.') for word in sent.split(' ')]
>>> atomic_nums = {}
>>> for i, elem in enumerate(elems, 1):
...     if i in [1, 5, 6, 7, 8, 9, 15, 16, 19]:
...         atomic_nums[elem[0]] = i
...     else:
...         atomic_nums[elem[:2]] = i
>>> print(atomic_nums)
{'H': 1, 'He': 2, 'Li': 3, 'Be': 4, 'B': 5, 'C': 6, 'N': 7, 'O': 8, 'F': 9, 'Ne': 10, 'Na': 11, 'Mi': 12, 'Al': 13, 'Si': 14, 'P': 15, 'S': 16, 'Cl': 17, 'Ar': 18, 'K': 19, 'Ca': 20}
```

# References

1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
