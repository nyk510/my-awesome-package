# My Awesome Package

GOGOGO!!!

## 概要

なにかしらの python パッケージをつくるときの最小要件を記載したリポジトリ。

## Requirements

local python environment (version >= 3.6)

## Setup (for venv)

Global な python 環境を汚さないように venv 内部で作業するようにします。

```bash
python -m venv .venv
source .venv/bin/activate
```

### Install My Package

CurrentDirectory `.` を起点として pip install を実行すると現在の python 環境に setup.py の内容のパッケージがインストールされます。

```bash
pip install -e .
```

### check install

ipython で確認。

```bash
08:01:39 in my-awesome-package on  master [?] via my-awesome-package 
➜ ipython 
Python 3.7.1 (default, Dec 14 2018, 19:28:38) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.24.1 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from goto_tools import version

In [2]: print(version.__version__)
0.510
```

## Test

### Setup

テスト用モジュールを install

```bash
pip install -e .[test]
```

#### 何が起こっているか

`setup.py` に記述された extra_require へ渡された dict の key == test となるものが install されます。今回のプロジェクトの場合

```python
def get_extra_requires():
    extras = {
        # テスト用のパッケージ
        'test': ['pytest'],
        # ドキュメント生成用パッケージ
        'document': ['sphinx', 'sphinx_rtd_theme']
    }
    return extras
```

で定義されているので `pytest` が install されます。

### テストの実行

```bash
pytest
```

```
08:10:49 in my-awesome-package on  master [?] via my-awesome-package took 17s 
➜ pytest                  
=========================================== test session starts ===========================================
platform linux -- Python 3.7.1, pytest-6.2.4, py-1.10.0, pluggy-0.13.1
rootdir: /home/nyker/workspace/my-awesome-package
collected 1 item                                                                                          

tests/test_version.py .                                                                             [100%]

============================================ 1 passed in 0.01s ============================================
```

## 新しい環境へ Install する

このリポジトリを github / gitlab へ upload していればすでに pip でインストールを行なうことが出来ます。

