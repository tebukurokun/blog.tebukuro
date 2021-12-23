---
title: 'pythonの仮想環境たち'
date: '2021-12-21'
tags: ['python', 'virtualenv', 'poetry']
draft: false
summary: 'pythonの仮想環境たちの使い方メモ'
---

# 概要

python の仮想環境管理の方法が複数あるので、それぞれの使用方法をメモ。

## 前提

Python の実行環境が既にあること。

## Poetry

node の package.json のように、使用するライブラリをファイルに記述し、`poetry install` するとライブラリをインストールできるもの。  
以下、[公式ドキュメント](https://python-poetry.org/)とほぼ同じ手順です。

### インストール

```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
```

homebrew を使用する場合はこれでも可能。

```
brew install poetry
```

- チェック

```
poetry --version
```

### プロジェクト作成

```
poetry new poetry-demo
```

以下のようなサンプルプロジェクトが作成される。

```
poetry-demo
├── pyproject.toml
├── README.rst
├── poetry_demo
│   └── __init__.py
└── tests
    ├── __init__.py
    └── test_poetry_demo.py
```

- 既にプロジェクトがある場合（カレントディレクトリにファイルが作成される）

```
poetry init
```

### プロジェクトのライブラリを管理

実行用のライブラリ(dependencies)を追加

```
poetry add <package>
```

開発用のライブラリ(dev-dependencies)を追加

```
poetry add -D <package>
```

pyproject.toml, poetry.lock に基づいてライブラリをインストール

```
poetry install
```

pyproject.toml に基づいてライブラリをアップデート

```
poetry update
```

- pyproject.toml の例

```toml
[tool.poetry]
name = "sample"
version = "0.1.0"
description = ""
authors = ["tebukuro"]

[tool.poetry.dependencies]
python = "^3.9"
pandas = "^1.3.3"

[tool.poetry.dev-dependencies]
pytest = "^6.2.5"

[build-system]
requires = ["poetry-core>=1.0.0"]
build-backend = "poetry.core.masonry.api"
```

### プロジェクトのディレクトリに仮想環境を作る

```
poetry config virtualenvs.in-project true
```

### その他コマンド

以下を参照。  
https://python-poetry.org/docs/cli/

## venv

python に標準で入っているツールのため、インストール不要。

### 使い方

環境作成

```
mkdir projectdir
cd projectdir
python -m venv venv
```

有効化

```
source venv/bin/activate
```

`pip install` しても仮想環境にのみインストールされるようになる。

### requirements.txt について

pip install するライブラリを管理するファイル。（ファイル名はなんでもいい）

- requirements.txt を作成  
  インストールされているライブラリがファイルに出力される。

```
pip freeze > requirements.txt
```

- requirements.txt に基づいてインストール

```
pip install -r requirements.txt
```

- requirements.txt の例

```requirements.txt
numpy==1.21.3
pandas==1.3.4
```
