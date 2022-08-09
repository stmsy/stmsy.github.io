---
title: Chapter 1. Warm-up
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.9
classes: wide
---

## 00. 文字列の逆順

### 文字列 ```"stressed"``` の文字を逆に（末尾から先頭に向かって）並べた文字列を得よ.

```python
>>> word = "stressed"
>>> print(word[::-1])
desserts
```

## 01. 「パタトクカシーー」

「```パタトクカシーー```」という文字列の1, 3, 5, 7文字目を取り出して連結した文字列を得よ.

```python
>>> word = "パタトクカシーー"
>>> print(word[::2])
パトカー
```
