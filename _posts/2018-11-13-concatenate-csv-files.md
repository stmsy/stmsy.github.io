---
title: Concatenate Multiple CSV Files
tags:
  - macOS
  - CSV
classes: wide
---

## Prerequisite

If you work with macOS, ```gnu-sed``` should be installed from Homebrew.

## Concatenate into a Single File

Suppose for simplicity that two CSV files ```file1.csv``` and ```file2.csv``` share the same header as follows:

```
# file1.csv
column1,column2,column3
foo1,bar1,baz1
foo2,bar2,baz2
```

```
# file2.csv
column1,column2,column3
foo3,bar3,baz3
```

To concatenate those files into a single CSV file, run the following commands

```bash
$ awk 'FNR > 1' *.csv > concatenated.csv
$ HEADER=`head -n 1 file1.csv`; gsed -i "1i$HEADER" concatenated.csv
```

and you will get

```
# concatenated.csv
column1,column2,column3
foo1,bar1,baz1
foo2,bar2,baz2
foo3,bar3,baz3
```

as expected.

