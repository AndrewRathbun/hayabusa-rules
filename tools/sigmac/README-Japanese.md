# SIGMAからHayabusaルールへの自動変換

[\[English\]](README.md) | [**日本語**]

[![python](https://img.shields.io/badge/python-3.8-blue)](https://www.python.org/)
![version](https://img.shields.io/badge/Platform-Win-green)
![version](https://img.shields.io/badge/Platform-Lin-green)
![version](https://img.shields.io/badge/Platform-Mac-green)

`hayabusa.py` はSigmaルールをHayabusaルールに変換する`sigmac`のバックエンドです。
Sigmaの持つ多くの検知ルールをHayabusaのルールセットに追加することでルールを作成する手間を省くことができます。

## 事前に変換されたSigmaルールについて

Sigmaからhayabusa形式に変換されたルールが`./rules/sigma`ディレクトリに用意されています。 
ローカル環境で新しいルールをテストしたり、Sigmaの最新のルールを変換したりしたい場合は、以下のドキュメンテーションをご参考下さい。

## Pythonの環境依存

Python 3.8以上と次のモジュールが必要です：`pyyaml`、`ruamel.yaml`、`requests` 
以下のコマンドでインストール可能です。

```sh
pip3 install -r requirements.txt
```

## Sigmaについて

[https://github.com/SigmaHQ/sigma](https://github.com/SigmaHQ/sigma)

## 環境設定

hayabusa.pyはSigmaリポジトリの中にある`sigmac`を使います。
事前に任意のディレクトリにSigmaリポジトリをcloneしてください。

```sh
git clone https://github.com/SigmaHQ/sigma.git
```

## 使い方

Sigmaレポジトリのパスが書いてある`$sigma_path`という環境変数を設定して、hayabusaをSigmaのbackendとして登録します:

```sh
export sigma_path=/path/to/sigma_repository
cp hayabusa.py $sigma_path/tools/sigma/backends
cp convert.py $sigma_path
```

* 注意：`/path/to/sigma_repository`そのままではなくて、自分のSigmaレポジトリのパスを指定してください。

### ルールの変換
`convert.py`を実行することでルールの変換が実行されます。変換されたルールは`hayabusa_rules`フォルダに作成されます。

```sh
cd $sigma_path
python3 convert.py
```

## 現在サポートされていないルール

以下のルールは、まだ実装されていないaggregation operator (`|near`)が含まれているため、現在は自動変換できません。

```
sigma/rules/windows/builtin/win_susp_samr_pwset.yml
sigma/rules/windows/image_load/sysmon_mimikatz_inmemory_detection.yml
sigma/rules/windows/process_creation/process_creation_apt_turla_commands_medium.yml
```

## Sigmaルールのパースエラーについて

一部のルールは変換できたものの、パースエラーが発生しています。
これらのバグは引き続き修正していきますが、当面はSigmaのルールの大部分は動作しますので、今のところエラーは無視してください。