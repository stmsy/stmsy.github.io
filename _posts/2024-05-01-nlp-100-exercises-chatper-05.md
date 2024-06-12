---
title: Chapter 5 Syntactic Parsing
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.12
classes: wide
use_math: true
---

夏目漱石の小説『吾輩は猫である』の文章（[`neko.txt`](http://www.cl.ecei.tohoku.ac.jp/nlp100/data/neko.txt)）を CaboCha を使って係り受け解析し, その結果を neko.txt.cabocha というファイルに保存せよ. このファイルを用いて, 以下の問に対応するプログラムを実装せよ.

```shell
>>> from pathlib import Path
>>> import CaboCha
>>> import requests
>>> NEKO_TEXT = 'neko.txt'
>>> NEKO_TEXT_URL = f'http://www.cl.ecei.tohoku.ac.jp/nlp100/data/{NEKO_TEXT}'
>>> SYN_PARSED_NEKO_TEXT_FILAPTH = Path(f'./{NEKO_TEXT}.cabocha')
>>> response = requests.get(NEKO_TEXT_URL)
>>> lines = (response.content.decode('utf-8')
>>>                          .split())[1:]  # Ignore the beginning of document
>>> syn_parsed_lines = []
>>> c = CaboCha.Parser()
>>> for line in lines:
...     tree = c.parse(line)
...     syn_parsed_line = tree.toString(CaboCha.FORMAT_LATTICE)
...     syn_parsed_lines.append(syn_parsed_line)
>>> with SYN_PARSED_NEKO_TEXT_FILAPTH.open('w') as f:
...     f.writelines(syn_parsed_lines)
```

## 40. 係り受け解析結果の読み込み（形態素）

形態素を表すクラス `Morph` を実装せよ. このクラスは表層形（`surface`）, 基本形（`base`）, 品詞（`pos`）, 品詞細分類1（`pos1`）をメンバ変数に持つこととする. さらに, CaboCha の解析結果（neko.txt.cabocha）を読み込み 各文を `Morph` オブジェクトのリストとして表現し, 3文目の形態素列を表示せよ.

## 41. 係り受け解析結果の読み込み（文節・係り受け）

[40](https://stmsy.github.io/nlp-100-exercises-chatper-05/#40-%E4%BF%82%E3%82%8A%E5%8F%97%E3%81%91%E8%A7%A3%E6%9E%90%E7%B5%90%E6%9E%9C%E3%81%AE%E8%AA%AD%E3%81%BF%E8%BE%BC%E3%81%BF%E5%BD%A2%E6%85%8B%E7%B4%A0)に加えて, 文節を表すクラス `Chunk` を実装せよ. このクラスは形態素（`Morph` オブジェクト）のリスト（`morphs`）, 係り先文節インデックス番号（`dst`）, 係り元文節インデックス番号のリスト（`srcs`）をメンバ変数に持つこととする. さらに, 入力テキストの CaboCha の解析結果を読み込み, 1文を `Chunk` オブジェクトのリストとして表現し, 8文目の文節の文字列と係り先を表示せよ. 第5章の残りの問題では, ここで作ったプログラムを活用せよ.

設問40, 41の処理を以下にまとめる.

```
>>> from collections import defaultdict
>>> from pprint import pprint
>>> import re
>>> from pydantic import BaseModel, NonNegativeInt
>>> class Morph(BaseModel):
>>>     surface: str
>>>     base: str
>>>     pos: str
>>>     pos1: str
>>> class Chunk(BaseModel):
>>>     index: NonNegativeInt | None = None
>>>     morphs: list[Morph] | None = None
>>>     dst: NonNegativeInt | None = None
>>>     srcs: list[NonNegativeInt] | None = None
>>> POS_TAG = ','.join(['(.+)'] * 9)
>>> MECAB_PATTERN = re.compile(f'(.+)\t{POS_TAG}')
>>> CHUNK_TAG = r'\* (\d+) (-*\d+)(\D) (\d+)/(\d+) '
>>> CABOCHA_PATTERN = re.compile(CHUNK_TAG)
>>> with SYN_PARSED_NEKO_TEXT_FILAPTH.open() as f:
>>>     text = f.read()
>>>     sentences = text.split('EOS\n')
>>> syn_parsed_sentences = {}
>>> for i, sentence in enumerate(sentences[:-1]):
>>>     lines = sentence.split('\n')[:-1]
>>>     syn_parsed_chunks = []
>>>     pos_tagged_tokens = defaultdict(list)
>>>     dep_structure = defaultdict(list)
>>>     for line in lines:
>>>         c = CABOCHA_PATTERN.match(line)
>>>         m = MECAB_PATTERN.match(line)
>>>         if c:
>>>             index, dst = int(c.group(1)), int(c.group(2))
>>>             dst = dst if dst >= 0 else None
>>>             dep_structure[dst].append(index)
>>>             chunk = Chunk(index=index, dst=dst)
>>>             syn_parsed_chunks.append(chunk)
>>>         if m:
>>>             morph = Morph(surface=m.group(1),
>>>                           base=m.group(8),
>>>                           pos=m.group(2),
>>>                           pos1=m.group(3))
>>>             pos_tagged_tokens[index].append(morph)
>>>     for syn_parsed_chunk in syn_parsed_chunks:
>>>         index = syn_parsed_chunk.index
>>>         syn_parsed_chunk.morphs = pos_tagged_tokens[index]
>>>         syn_parsed_chunk.srcs = dep_structure[index]
>>>     syn_parsed_sentences[i] = syn_parsed_chunks
>>> syn_parsed_chunks = syn_parsed_sentences[2]
>>> for syn_parsed_chunk in syn_parsed_chunks:
>>>     pprint(syn_parsed_chunk.morphs)
[Morph(surface='どこ', base='どこ', pos='名詞', pos1='代名詞'),
 Morph(surface='で', base='で', pos='助詞', pos1='格助詞')]
[Morph(surface='生れ', base='生れる', pos='動詞', pos1='自立'),
 Morph(surface='た', base='た', pos='助動詞', pos1='*'),
 Morph(surface='か', base='か', pos='助詞', pos1='副助詞／並立助詞／終助詞')]
[Morph(surface='とんと', base='とんと', pos='副詞', pos1='一般')]
[Morph(surface='見当', base='見当', pos='名詞', pos1='サ変接続'),
 Morph(surface='が', base='が', pos='助詞', pos1='格助詞')]
[Morph(surface='つか', base='つく', pos='動詞', pos1='自立'),
 Morph(surface='ぬ', base='ぬ', pos='助動詞', pos1='*'),
 Morph(surface='。', base='。', pos='記号', pos1='句点')]
>>> syn_parsed_chunks = syn_parsed_sentences[7]
>>> for syn_parsed_chunk in syn_parsed_chunks:
>>>     surfaces = list(map(lambda x: x.surface, syn_parsed_chunk.morphs))
>>>     pprint(f"文節: {''.join(surfaces)}, 係り先: {syn_parsed_chunk.dst}")
'文節: しかし, 係り先: 9'
'文節: その, 係り先: 2'
'文節: 当時は, 係り先: 5'
'文節: 何という, 係り先: 4'
'文節: 考も, 係り先: 5'
'文節: なかったから, 係り先: 9'
'文節: 別段, 係り先: 7'
'文節: 恐し, 係り先: 9'
'文節: いとも, 係り先: 9'
'文節: 思わなかった。, 係り先: None'
```

## 42. 係り元と係り先の文節の表示

係り元の文節と係り先の文節のテキストをタブ区切り形式ですべて抽出せよ. ただし, 句読点などの記号は出力しないようにせよ.

## 43. 名詞を含む文節が動詞を含む文節に係るものを抽出

名詞を含む文節が, 動詞を含む文節に係るとき, これらをタブ区切り形式で抽出せよ. ただし, 句読点などの記号は出力しないようにせよ.

## 44. 係り受け木の可視化

与えられた文の係り受け木を有向グラフとして可視化せよ. 可視化には, 係り受け木を [DOT](http://ja.wikipedia.org/wiki/DOT%E8%A8%80%E8%AA%9E) 言語に変換し, [Graphviz](http://www.graphviz.org/) を用いるとよい. また, Python から有向グラフを直接的に可視化するには, [pydot](https://code.google.com/p/pydot/) を使うとよい.

## 45. 動詞の格パターンの抽出

今回用いている文章をコーパスと見なし, 日本語の述語が取りうる格を調査したい. 動詞を述語, 動詞に係っている文節の助詞を格と考え, 述語と格をタブ区切り形式で出力せよ. ただし, 出力は以下の仕様を満たすようにせよ.

- 動詞を含む文節において，最左の動詞の基本形を述語とする
- 述語に係る助詞を格とする
- 述語に係る助詞（文節）が複数あるときは, すべての助詞をスペース区切りで辞書順に並べる

「吾輩はここで始めて人間というものを見た」という例文（neko.txt.cabocha の8文目）を考える. この文は「始める」と「見る」の2つの動詞を含み,「始める」に係る文節は「ここで」,「見る」に係る文節は「吾輩は」と「ものを」と解析された場合は, 次のような出力になるはずである.

```
始める  で
見る    は を
```

このプログラムの出力をファイルに保存し. 以下の事項を UNIX コマンドを用いて確認せよ.

- コーパス中で頻出する述語と格パターンの組み合わせ
- 「する」「見る」「与える」という動詞の格パターン（コーパス中で出現頻度の高い順に並べよ）

## 46. 動詞の格フレーム情報の抽出

[45](https://stmsy.github.io/nlp-100-exercises-chatper-05/#45-%E5%8B%95%E8%A9%9E%E3%81%AE%E6%A0%BC%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E3%81%AE%E6%8A%BD%E5%87%BA)のプログラムを改変し, 述語と格パターンに続けて項（述語に係っている文節そのもの）をタブ区切り形式で出力せよ. [45](https://stmsy.github.io/nlp-100-exercises-chatper-05/#45-%E5%8B%95%E8%A9%9E%E3%81%AE%E6%A0%BC%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E3%81%AE%E6%8A%BD%E5%87%BA)の仕様に加えて, 以下の仕様を満たすようにせよ.

- 項は述語に係っている文節の単語列とする（末尾の助詞を取り除く必要はない）
- 述語に係る文節が複数あるときは，助詞と同一の基準・順序でスペース区切りで並べる

「吾輩はここで始めて人間というものを見た」という例文（neko.txt.cabocha の8文目）を考える. この文は「始める」と「見る」の2つの動詞を含み,「始める」に係る文節は「ここで」,「見る」に係る文節は「吾輩は」と「ものを」と解析された場合は, 次のような出力になるはずである.

```
始める  で      ここで
見る    は を   吾輩は ものを
```

## 47. 機能動詞構文のマイニング

動詞のヲ格にサ変接続名詞が入っている場合のみに着目したい. [46](https://stmsy.github.io/nlp-100-exercises-chatper-05/#46-%E5%8B%95%E8%A9%9E%E3%81%AE%E6%A0%BC%E3%83%95%E3%83%AC%E3%83%BC%E3%83%A0%E6%83%85%E5%A0%B1%E3%81%AE%E6%8A%BD%E5%87%BA)のプログラムを以下の仕様を満たすように改変せよ．

- 「サ変接続名詞+を（助詞）」で構成される文節が動詞に係る場合のみを対象とする
- 述語は「サ変接続名詞+を+動詞の基本形」とし, 文節中に複数の動詞があるときは，最左の動詞を用いる
- 述語に係る助詞（文節）が複数あるときは, すべての助詞をスペース区切りで辞書順に並べる
- 述語に係る文節が複数ある場合は, すべての項をスペース区切りで並べる（助詞の並び順と揃えよ）
- 例えば「別段くるにも及ばんさと、主人は手紙に返事をする。」という文から，以下の出力が得られるはずである


```
返事をする      と に は        及ばんさと 手紙に 主人は
```

このプログラムの出力をファイルに保存し, 以下の事項をUNIXコマンドを用いて確認せよ.

- コーパス中で頻出する述語（サ変接続名詞+を+動詞）
- コーパス中で頻出する述語と助詞パターン

## 48. 名詞から根へのパスの抽出

文中のすべての名詞を含む文節に対し, その文節から構文木の根に至るパスを抽出せよ. ただし, 構文木上のパスは以下の仕様を満たすものとする.

- 各文節は（表層形の）形態素列で表現する
- パスの開始文節から終了文節に至るまで, 各文節の表現を"`->`"で連結する

「吾輩はここで始めて人間というものを見た」という文（neko.txt.cabocha の8文目）から, 次のような出力が得られるはずである.

```
吾輩は -> 見た
ここで -> 始めて -> 人間という -> ものを -> 見た
人間という -> ものを -> 見た
ものを -> 見た
```

## 49. 名詞間の係り受けパスの抽出

文中のすべての名詞句のペアを結ぶ最短係り受けパスを抽出せよ. ただし, 名詞句ペアの文節番号が $i$ と $j$（$i < j$）のとき, 係り受けパスは以下の仕様を満たすものとする.

- 問題[48](https://stmsy.github.io/nlp-100-exercises-chatper-05/#48-%E5%90%8D%E8%A9%9E%E3%81%8B%E3%82%89%E6%A0%B9%E3%81%B8%E3%81%AE%E3%83%91%E3%82%B9%E3%81%AE%E6%8A%BD%E5%87%BA)と同様に, パスは開始文節から終了文節に至るまでの各文節の表現（表層形の形態素列）を"`->`"で連結して表現する
- 文節 $i$ と $j$ に含まれる名詞句はそれぞれ，XとYに置換する

また, 係り受けパスの形状は, 以下の2通りが考えられる.

- 文節 $i$ から構文木の根に至る経路上に文節 $j$ が存在する場合: 文節 $i$ から文節 $j$ のパスを表示
- 上記以外で，文節 $i$ と文節 $j$ から構文木の根に至る経路上で共通の文節 $k$ で交わる場合: 文節 $i$ から文節 $k$ に至る直前のパスと文節 $j$ から文節 $k$ に至る直前までのパス, 文節kの内容を"`|`"で連結して表示

例えば,「吾輩はここで始めて人間というものを見た。」という文（neko.txt.cabocha の8文目）から, 次のような出力が得られるはずである.

```
Xは | Yで -> 始めて -> 人間という -> ものを | 見た
Xは | Yという -> ものを | 見た
Xは | Yを | 見た
Xで -> 始めて -> Y
Xで -> 始めて -> 人間という -> Y
Xという -> Y
```

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
