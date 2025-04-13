# gemma-3-4b-vqa

# gemma-3-4b-vqa

このリポジトリでは、[SakanaAI/JA-VG-VQA-500](https://huggingface.co/datasets/SakanaAI/JA-VG-VQA-500) データセットと Google の Gemma3 モデル ([google/gemma-3-4b-it](https://huggingface.co/google/gemma-3-4b-it)) を利用し、  
日本語ビジョンランゲージ（VQA: Visual Question Answering）推論を行うためのサンプルコードを提供しています。

---

## ファイル構成

- **main.py**  
  JA-VG-VQA-500 データセットから画像データと対応する複数の Q&A を取得し、Gemma3 へ入力 → モデル出力を JSONL 形式で保存するサンプルスクリプト。

---

## 環境構築手順

### 1. Python のインストール
Python 3.8 以上を推奨します（3.7 以下の場合、一部のライブラリで問題が起きる可能性があります）。

### 2. 必要パッケージのインストール
以下のように `pip` を利用してインストールします:

```bash
pip install --upgrade pip
pip install torch transformers datasets Pillow
