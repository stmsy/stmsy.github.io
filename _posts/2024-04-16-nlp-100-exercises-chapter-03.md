---
title: Chapter 3 Regular Expressions
tags:
  - Natural Language Processing
  - Japanese
  - Python 3.12
classes: wide
---

Wikipedia の記事を以下のフォーマットで書き出したファイル [`jawiki-country.json.gz`](https://www.cl.ecei.tohoku.ac.jp/nlp100/data/jawiki-country.json.gz) がある．

- 1行に1記事の情報が JSON 形式で格納される
- 各行には記事名が "title" キーに，記事本文が "text" キーの辞書オブジェクトに格納され，そのオブジェクトが JSON 形式で書き出される
- ファイル全体は `gzip` で圧縮される

以下の処理を行うプログラムを作成せよ．

## 20. JSONデータの読み込み
Wikipedia 記事の JSON ファイルを読み込み，「イギリス」に関する記事本文を表示せよ．問題21-29 では，ここで抽出した記事本文に対して実行せよ．

```shell
>>> from gzip import GzipFile
>>> from io import BytesIO
>>> import json
>>> from pprint import pprint
>>> import requests
>>> GZIPPED_JSON_FILE_URL = 'http://www.cl.ecei.tohoku.ac.jp/nlp100/data/jawiki-country.json.gz'
>>> UK = 'イギリス'
>>> response = requests.get(GZIPPED_JSON_FILE_URL)
>>> buffered = BytesIO(response.content)
>>> with GzipFile(fileobj=buffered) as gf:
...     articles = list(map(lambda x: json.loads(x.decode('utf-8')), gf.readlines()))
>>> wikipedia = {}
>>> for article in articles:
...     title = article['title']
...     text = article['text']
...     wikipedia[title] = text
>>> pprint(wikipedia[UK])
{'text': '{{redirect|UK}}\n'
         '{{基礎情報 国\n'
         '|略名 = イギリス\n'
         '|日本語国名 = グレートブリテン及び北アイルランド連合王国\n'
         '|公式国名 = {{lang|en|United Kingdom of Great Britain and Northern '
         'Ireland}}<ref>英語以外での正式国名:<br/>\n'
         '*{{lang|gd|An Rìoghachd Aonaichte na Breatainn Mhòr agus Eirinn mu '
         'Thuath}}（[[スコットランド・ゲール語]]）<br/>\n'
         '*{{lang|cy|Teyrnas Gyfunol Prydain Fawr a Gogledd '
         'Iwerddon}}（[[ウェールズ語]]）<br/>\n'
         '*{{lang|ga|Ríocht Aontaithe na Breataine Móire agus Tuaisceart na '
         'hÉireann}}（[[アイルランド語]]）<br/>\n'
         '*{{lang|kw|An Rywvaneth Unys a Vreten Veur hag Iwerdhon '
         'Glédh}}（[[コーンウォール語]]）<br/>\n'
         '*{{lang|sco|Unitit Kinrick o Great Breetain an Northren '
         'Ireland}}（[[スコットランド語]]）<br/>\n'
         '**{{lang|sco|Claught Kängrick o Docht Brätain an Norlin '
         'Airlann}}、{{lang|sco|Unitet Kängdom o Great Brittain an Norlin '
         'Airlann}}（アルスター・スコットランド語）</ref>\n'
...
```

## 21. カテゴリ名を含む行を抽出
記事中でカテゴリ名を宣言している行を抽出せよ．

```shell
>>> CATEGORY = 'Category'
>>> splitted_text_uk = raw_text_uk.replace('\n\n', '\n').split('\n')
>>> category_rows = [line for line in splitted_text_uk if CATEGORY in row]
>>> pprint(category_rows)
['[[Category:イギリス|*]]',
 '[[Category:英連邦王国|*]]',
 '[[Category:G8加盟国]]',
 '[[Category:欧州連合加盟国]]',
 '[[Category:海洋国家]]',
 '[[Category:君主国]]',
 '[[Category:島国|くれいとふりてん]]',
 '[[Category:1801年に設立された州・地域]]']
```

## 22. カテゴリ名の抽出
記事のカテゴリ名を（行単位ではなく名前で）抽出せよ．

```shell
>>> import re
>>> PATTERN_FOR_CATEGORY = r'\[\[Category:(.*?)[\|\]].*?'
>>> category_names = []
>>> for category_row in category_rows:
...     m = re.search(PATTERN_FOR_CATEGORY, category_row)
...     if m:
...         category_name = m.group(1)
...         category_names.append(category_name)
>>> pprint(category_names)
['イギリス', '英連邦王国', 'G8加盟国', '欧州連合加盟国', '海洋国家', '君主国', '島国', '1801年に設立された州・地域']
```

## 23. セクション構造
記事中に含まれるセクション名とそのレベル（例えば "== セクション名 ==" なら1）を表示せよ．

```shell
>>> PATTERN_FOR_SECTIONS = r'(={2,})\s?(.*?)\s?={2,}'
>>> for line in splitted_text_uk:
...     m = re.search(PATTERN_FOR_SECTIONS, line)
...     if m:
...         section_level = len(m.group(1)) - 1
...         section_name = m.group(2)
...         print(section_name, section_level, sep='\t')
国名	1
歴史	1
地理	1
気候	2
政治	1
...
```

## 24. ファイル参照の抽出
記事から参照されているメディアファイルをすべて抜き出せ．

```shell
>>> PATTERN_FOR_MEDIA_FILES = r'.*(ファイル|File):(.*?)(\|.*?)'
>>> media_files = []
>>> for line in splitted_text_uk:
...     m = re.search(PATTERN_FOR_MEDIA_FILES, line)
...     if m:
...         media_file = m.group(2)
...         media_files.append(media_file)
>>> pprint(media_files)
['Royal Coat of Arms of the United Kingdom.svg',
 'Battle of Waterloo 1815.PNG',
 'The British Empire.png',
 'Uk topo en.jpg',
 'BenNevis2005.jpg',
...
```

## 25. テンプレートの抽出
記事中に含まれる「基礎情報」テンプレートのフィールド名と値を抽出し，辞書オブジェクトとして格納せよ．

## 26. 強調マークアップの除去
[25](https://stmsy.github.io/nlp-100-exercises-chapter-03/#25-%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%81%AE%E6%8A%BD%E5%87%BA)の処理時に，テンプレートの値から MediaWiki の強調マークアップ（弱い強調，強調，強い強調のすべて）を除去してテキストに変換せよ（参考: [マークアップ早見表](http://ja.wikipedia.org/wiki/Help:%E6%97%A9%E8%A6%8B%E8%A1%A8)）．

## 27. 内部リンクの除去
[26](https://stmsy.github.io/nlp-100-exercises-chapter-03/#26-%E5%BC%B7%E8%AA%BF%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E9%99%A4%E5%8E%BB)の処理に加えて，テンプレートの値から MediaWiki の内部リンクマークアップを除去し，テキストに変換せよ（参考: [マークアップ早見表](http://ja.wikipedia.org/wiki/Help:%E6%97%A9%E8%A6%8B%E8%A1%A8)）．

## 28. MediaWiki マークアップの除去
[27](https://stmsy.github.io/nlp-100-exercises-chapter-03/#28-mediawiki%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E9%99%A4%E5%8E%BB)の処理に加えて，テンプレートの値から MediaWiki マークアップを可能な限り除去し，国の基本情報を整形せよ．

設問25-28の処理を以下にまとめる.

```shell
>>> PATTERN_FOR_MAIN = r"\|(.+?) = (.+)"
>>> PATTERN_FOR_EMPHASIS = r"\'{2,5}"
>>> PATTERN_FOR_BRACES = r".*\{\{.+\|(.+)\|(.+)\}\}"
>>> PATTERN_FOR_SINGLE_BLOCKS = r".*\[\[(.+)\]\].*"
>>> PATTERN_FOR_DOUBLE_BLOCKS = r"\[\[(.+?)\]\].*\[\[(.+?)\]\]"
>>> PATTERN_FOR_REF = r"(.+?)<ref.+>$"
>>> PATTERN_FOR_BR = r"(.+?)<br.+"
>>> PATTERN_FOR_MEDIA_FILES = r"(ファイル|File):(.+?)\|.+"
>>> basic_info = {}
>>> start = splitted_text_uk.index('{{基礎情報 国') + 1
>>> end = splitted_text_uk.index('}}') - 2
>>> for line in splitted_text_uk[start:end+1]:
...     line = re.sub(PATTERN_FOR_EMPHASIS, '',  line)
...     if line[0] == '|':
...         if line[1:5] != '公式国名':
...             m = re.search(PATTERN_FOR_MAIN, line)
...             key, value = m.group(1), m.group(2)
...             if 'ref' in value:
...                 m = re.search(PATTERN_FOR_REF, value)
...                 value = m.group(1)
...             if 'br' in value:
...                 m = re.search(PATTERN_FOR_BR, value)
...                 value = m.group(1)
...             if '[[' in value:
...                 if key not in ('確立形態1', '確立年月日1', 'ccTLD'):
...                     m = re.search(PATTERN_FOR_SINGLE_BLOCKS, value)
...                     value = m.group(1)
...                     if '|' in value:
...                         if value[:5] == 'ファイル:':
...                             m = re.search(PATTERN_FOR_MEDIA_FILES, value)
...                             value = m.group(2)
...                         else:
...                             value = list(value.split('|'))
...                 else:
...                     m = re.search(PATTERN_FOR_DOUBLE_BLOCKS, value)
...                     value = list(m.groups())
...             basic_info[key] = value
...         else:
...             m = re.search(PATTERN_FOR_BRACES, line)
...             key, value = m.group(1), m.group(2)
...             basic_info['公式国名'] = {key: value}
...     elif line[:3] == '*{{':
...         # Capture the country name in other languages
...         m = re.search(PATTERN_FOR_BRACES, line)
...         key, value = m.group(1), m.group(2)
...         if key != 'sco':
...             basic_info['公式国名'].update({key: value})
...         else:
...             basic_info['公式国名'].update({key: [value]})
...     elif line[:3] == '**{':
...         # Capture another two country names in Scottish
...         for substr in line.split('、'):
...             m = re.search(PATTERN_FOR_BRACES, substr)
...             key, value = m.group(1), m.group(2)
...             basic_info['公式国名'][key].append(value)
>>> pprint(basic_info)
{'GDP/人': '36,727',
 'GDP値': '2兆3162億',
 'GDP値MER': '2兆4337億',
 'GDP値元': '1兆5478億',
 'GDP統計年': '2012',
... 
```

## 29. 国旗画像の URL を取得する
テンプレートの内容を利用し，国旗画像の URL を取得せよ．（ヒント: [MediaWiki API](http://www.mediawiki.org/wiki/API:Main_page/ja) の [imageinfo](http://www.mediawiki.org/wiki/API:Properties/ja#imageinfo_.2F_ii) を呼び出して，ファイル参照を URL に変換すればよい）

# References
1. Okazaki, N. (2015). *言語処理100本ノック 2015* [Natural Language Processing 100 Exercises 2015]. Retrieved from http://www.cl.ecei.tohoku.ac.jp/nlp100/
2. Okazaki, N. (2020). *言語処理100本ノック 2020* [Natural Language Processing 100 Exercises 2020]. Retrieved from https://nlp100.github.io/ja/
