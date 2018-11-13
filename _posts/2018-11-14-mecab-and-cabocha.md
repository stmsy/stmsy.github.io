---
title: Install MeCab and CaboCha in Debian 8
tags:
  - Linux
  - Debian
  - Jessie
  - Natural Language Processing
  - MeCab
  - CaboCha
classes: wide
---

## MeCab

[MeCab](http://taku910.github.io/mecab/) is an open source Japanese Part-Of-Speech tagging engine developed and maintained by Dr. [Taku Kudo](http://chasen.org/~taku/index.html.en).

## Requirements

1. `g++ 3.4.3` or later
2. `iconv`

## Install from Source

Use the `tar` command to extract `mecab-0.996.tar.gz`.

```bash
$ tar zxvf mecab-0.996.tar.gz
```

`cd` into `mecab-0.966` and use the following commands to install MeCab.

```bash
$ cd mecab-0.996
$ ./configure --with-charset=UTF8
$ make
$ make check
$ sudo make install
```

Use again the `tar` command to extract `mecab-ipadic-2.7.0-20070801.tar.gz`, the Japanese dictionary for MeCab. Then `cd` into `mecab-ipadic-2.7.0-20070801` and install the `ipadic` dictionary as follows. 

```bash
$ tar zxvf mecab-ipadic-2.7.0-20070801.tar.gz
$ cd mecab-ipadic-2.7.0-20070801
$ ./configure --with-charset=UTF8
$ make
$ sudo make install
```

If `./configure --with-charset=UTF8` gives an error, try the following command

```bash
sudo ldconfig
```

to update the shared library system.

Refer to the following in case you want to use MeCab in Python.

```bash
$ tar zxvf mecab-python-0.996.tar.gz
$ cd mecab-python-0.996
$ python setup.py build
$ python setup.py install
```

## CaboCha

[CaboCha](http://taku910.github.io/cabocha/) is an open source Japanese depedency parser also developed and maintained by Dr. Kudo.

## Requirements

1. MeCab 0.993 or later
2. One of the follwing dictionary for MeCab: `mecab-ipadic`, `mecab-jamandic` and `unidic`

## Install from Source

Run the commands below to install the conditional random fields toolkit CRF++ used as dependency for CaboCha.

```bash
$ tar zxvf CRF++-0.58.tar.gz
$ cd CRF++-0.58
$ ./configure
$ make
$ sudo make install
```

Now is the time to install CaboCha. Use the `tar` command to extract `cabocha-0.67.tar.bz2`

```bash
tar jxvf cabocha-0.67.tar.bz2
```

Move to `cabocha-0.67` and use the following commands to install CaboCha.

```bash
$ tar jxvf cabocha-0.67.tar.gz
$ cd cabocha-0.67
$ ./configure --with-charset=UTF8
$ make
$ make check
$ sudo make install
```

Furthermore

```bash
$ cd python
$ python setup.py build
$ python setup.py install
```

if you want to use CaboCha from Python. After installing the package, you may be required to execute the `ldconfig` command again in case you fail to import the CaboCha module from the Python intepreter.
