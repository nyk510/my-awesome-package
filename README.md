# GOTO Awesome Package

GOGOGO!!!

## 概要

なにかしらの python パッケージをつくるときの最小要件を記載したリポジトリ。

## Requirements

local python environment (version >= 3.6)

## Setup

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

上記をこのプロジェクトのルートで実行すると `goto_tools` が install されます。

### Check Install

```bash
08:01:39 in my-awesome-package on  master [?] via my-awesome-package 
➜ ipython 
Python 3.7.1 (default, Dec 14 2018, 19:28:38) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.24.1 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from goto_tools import version

In [2]: print(version.__version__)
0.511
```

## 新しい環境へ Install する

### git を使った install

リポジトリを github / gitlab へ upload していれば `git+<my-repo-url>` でインストールを行なうことが出来ます。gitlab の url は `https://gitlab.com/nyker510/my-awesome-package` ですので、以下で install 出来ます。

```bash
pip install git+https://gitlab.com/nyker510/my-awesome-package
```

### pypi 経由での install (pip install my-package-name 形式)

pypi 経由での公開をすると `pip install my-package-name` でインストールができ pypi 上にも readme が展開されて表示されるようになります。かっこいいですね。
公開のためには

1. pypi でアカウントを作成
2. 作成したアカウントのログイン情報、または APITOKEN を取得
3. `twine` を使って pypi への upload

という手順を踏みます。詳しくは以下のURLなど参考にしてください。

* Python: Twine を使って PyPI にパッケージをアップロードする: https://blog.amedama.jp/entry/2017/12/31/175036
* Packaging Python Projects: https://packaging.python.org/tutorials/packaging-projects/

## Test

### Setup

テスト用モジュールを install

```bash
pip install -e .[test]
```

#### [note] 何が起こっているか

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

## CI

* TODO
