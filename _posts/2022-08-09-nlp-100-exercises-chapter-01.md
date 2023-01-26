---
title: Chapter 1 Warm-up
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.9
classes: wide
---

## 00. 文字列の逆順

文字列 "stressed" の文字を逆に（末尾から先頭に向かって）並べた文字列を得よ.

```shell
>>> word = "stressed"
>>> print(word[::-1])
desserts
```

## 01. 「パタトクカシーー」

"パタトクカシーー"という文字列の1, 3, 5, 7文字目を取り出して連結した文字列を得よ.

```shell
>>> word = "パタトクカシーー"
>>> print(word[::2])
パトカー
```

## 02. 「パトカー」＋「タクシー」＝「パタトクカシーー」

"パトカー"＋"タクシー"の文字を先頭から交互に連結して文字列"パタトクカシーー"を得よ.

```shell
>>> first, second = "パトカー", "タクシー"
>>> concated = ["" for _ in range(len(first + second))]
>>> concated[::2] = list(first)
>>> concated[1::2] = list(second)
>>> word = "".join(concated)
>>> print(word)
パタトクカシーー
```

## 03. 円周率

"Now I need a drink, alcoholic of course, after the heavy lectures involving quantum mechanics." という文を単語に分解し, 各単語の（アルファベットの）文字数を先頭から出現順に並べたリストを作成せよ.

```shell
>>> sent = ("Now I need a drink, alcoholic of course, after the heavy lectures "
...         "involving quantum mechanics.")
>>> words = [word.rstrip(',.') for word in sent.split(' ')]
>>> counts = [len(word) for word in words]
>>> print(counts)
[3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5, 8, 9, 7, 9]
```

## 04. 元素記号

"Hi He Lied Because Boron Could Not Oxidize Fluorine. New Nations Might Also Sign Peace Security Clause. Arthur King Can." という文を単語に分解し, 1, 5, 6, 7, 8, 9, 15, 16, 19番目の単語は先頭の1文字, それ以外の単語は先頭に2文字を取り出し, 取り出した文字列から単語の位置（先頭から何番目の単語か）への連想配列（辞書型もしくはマップ型）を作成せよ.

```shell
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

## 05. n-gram

与えられたシーケンス（文字列やリストなど）から n-gram を作る関数を作成せよ. この関数を用い, "I am an NLPer" という文から単語 bi-gram, 文字 bi-gram を得よ.

```python
from typing import List, Union


def get_n_gram(sent: str, n: int = 2, word_n_gram: bool = True) -> List[Union[str, List[str]]]:
    """Return a list of word or string n-grams."""
    words: List[str] = [word.rstrip(',.') for word in sent.split(' ')]
    n_gram: List[Union[str, List[str]]] = []
    if word_n_gram:
        num_words: int = len(words)
        if num_words <= n:
            n_gram += [words]
        else:
            for i in range(num_words-n+1):
                n_gram += [words[i:i+n]]
    else:
        string: str = "".join(words)
        len_string: int = len(string)
        if len_string <= n:
            n_gram += [[string]]
        else:
            for i in range(len_string-n+1):
                n_gram += [string[i:i+n]]
    return n_gram
```

```shell
>>> sent = "I am an NLPer"
>>> word_bi_gram = get_n_gram(sent)
>>> print(word_bi_gram)
[['I', 'am'], ['am', 'an'], ['an', 'NLPer']]
>>> str_bi_gram = get_n_gram(sent, n=2, word_n_gram=False)
>>> print(str_bi_gram)
['Ia', 'am', 'ma', 'an', 'nN', 'NL', 'LP', 'Pe', 'er']
```

## 06. 集合
"paraparaparadise" と "paragraph" に含まれる文字 bi-gram の集合を, それぞれ, ```X``` と ```Y``` として求め, ```X``` と ```Y``` の和集合, 積集合, 差集合を求めよ. さらに, 'se' という bi-gram が ```X``` および ```Y``` に含まれるかどうかを調べよ.

```shell
>>> X = set(get_n_gram("paraparaparadise", word_n_gram=False))
>>> Y = set(get_n_gram("paragraph", word_n_gram=False))
>>> X.union(Y)
{'ad', 'ag', 'ap', 'ar', 'di', 'gr', 'is', 'pa', 'ph', 'ra', 'se'}
>>> X.intersection(Y)
{'ap', 'ar', 'pa', 'ra'}
>>> X.difference(Y)
{'ad', 'di', 'is', 'se'}
>>> 'se' in X
True
>>> 'se' in Y
False
```

## 07. テンプレートによる文生成

引数 ```x```, ```y```, ```z``` を受け取り「```x``` 時の ```y``` は ```z```」という文字列を返す関数を実装せよ. さらに, ```x=12```, ```y="気温"```, ```z=22.4``` として，実行結果を確認せよ.

```python
def gen_sent(x: int, y: str, z: float) -> str:
    """Generate a simple template sentence."""
    return f"{x}時の{y}は{z}"
```

```shell
>>> gen_sent(x=12, y="気温", z=22.4)
12時の気温は22.4
```

## 08. 暗号文

与えられた文字列の各文字を, 以下の仕様で変換する関数 ```cipher``` を実装せよ.

- 英小文字ならば（219 - 文字コード）の文字に置換
- その他の文字はそのまま出力

この関数を用い, 英語のメッセージを暗号化・復号化せよ.

```python
from typing import List


def cipher(sent: str) -> str:
    """Cipher and decipher an English message."""
    ciphered: List[str] = []
    chars: List[str] = list(sent)
    for char in chars:
        if char.islower():
            ciphered += [chr(219 - ord(char))]
        else:
            ciphered += [char]
    return "".join(ciphered)
```

```shell
>>> cipher("Today is Monday.")
Tlwzb rh Mlmwzb.
>>> cipher("Tlwzb rh Mlmwzb.")
Today is Monday.
```

## 09. Typoglycemia

スペースで区切られた単語列に対して, 各単語の先頭と末尾の文字は残し, それ以外の文字の順序をランダムに並び替えるプログラムを作成せよ. ただし, 長さが4以下の単語は並び替えないこととする．適当な英語の文（例えば "I couldn't believe that I could actually understand what I was reading : the phenomenal power of the human mind ."）を与え, その実行結果を確認せよ.

```python
import random
from typing import List


def get_typoglycemia(text: str) -> str:
    """Return typoglycemia from an English text."""
    shuffled: List[str] = []
    tokens: List[str] = text.split(' ')
    first: str
    last: str
    substring: str
    for token in tokens:
        if len(token) > 4:
            first, last = token[0], token[-1]
            substring = token[1:-1]
            middle = "".join(random.sample(substring, len(substring)))
            shuffled += [first + middle + last]
        else:
            shuffled += [token]
    return " ".join(shuffled)
```

```shell
>>> text_orig = ("I couldn't believe that I could actually understand what I was "
...              "reading : the phenomenal power of the human mind .")
>>> text_typoglycemia = get_typoglycemia(text_orig)
>>> print(text_typoglycemia)
I cold'unt bleeive that I could autllacy ursndneatd what I was rnaeidg : the pemnoanhel peowr of the huamn mind .
```

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
