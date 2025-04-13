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






スクリプトでは、JA-VG-VQA-500 の test スプリットから順に (画像・質問) を読み込みます。

Pillow (PIL) の EXIF 処理によるエラーを回避するために decode=False を指定し、画像を raw bytes として読み込みます。

読み込んだバイナリ画像を一時ファイル (temp_***.jpg) に保存し、Gemma3 にそのファイルパスを渡して推論を行います。




スクリプトでは、JA-VG-VQA-500 の test スプリットから順に (画像・質問) を読み込みます。

Pillow (PIL) の EXIF 処理によるエラーを回避するために decode=False を指定し、画像を raw bytes として読み込んでいます。

読み込んだバイナリ画像を一時ファイルに保存 → Gemma3 にファイルパスを渡す形で推論を行います。

出力ファイル (gemma3_output.jsonl)
推論結果は gemma3_output.jsonl に書き出されます。内容は以下の項目を含む JSON 形式です。

image_id: 入力画像の ID

qa_id: 質問ごとのユニーク ID

url: 画像の外部 URL

question: 質問文

pred_answer: Gemma3 の推論回答

gt_answer: データセットのアノテーションとしての正解（比較用）

出力例（1 QA あたり1行の JSON 形式）
{
  "image_id": 100,
  "qa_id": 10674688,
  "url": "https://example.com/image.jpg",
  "question": "どんな天候ですか？",
  "pred_answer": "晴れの日",
  "gt_answer": "晴天"
}
