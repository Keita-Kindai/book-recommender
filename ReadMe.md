# 書籍推薦アルゴリズムの開発

## 概要
このプロジェクトは、自然言語処理（NLP）を用いた書籍推薦システムを開発したものです。ユーザーが入力したクエリに基づいて、ベクトル検索と感情分析を組み合わせた推薦アルゴリズムを実装しています。Gradioを用いたWebインターフェースで、簡単に書籍を検索・推薦できます。

## 背景
このプロジェクトは、大学の講義で自然言語処理を扱う授業を受講したことをきっかけに作成されました。そこでYouTubeに上がっていた動画の内容をもとに（リンク先は参考動画の部分に記述）、講義で学んだ知識を実際のアプリケーションに活用することを目的としています。主に以下のトピックについて学びました：
- Pandasの使い方とデータ前処理の方法
- Transformerとは何か（NLPモデルの基礎）
- HuggingFaceのpipelineの使い方
- Gradioの使い方（Webインターフェースの作成）
- ベクトルデータベースとは何か（Chromaを使用）

これらの知識を基に、書籍の説明文をベクトル化し、ユーザーのクエリとの類似度を計算して推薦するシステムを構築しました。

## 使用したライブラリ
- **pandas**: データ処理と分析
- **numpy**: 数値計算
- **dotenv**: 環境変数の管理
- **langchain_community**: ドキュメントローダー
- **langchain_openai**: OpenAIのEmbeddings API
- **langchain_text_splitters**: テキスト分割
- **langchain_chroma**: Chromaベクトルデータベース
- **gradio**: Webインターフェースの作成
- **rich**: コンソール出力の装飾
- **kagglehub**: Kaggleデータセットのダウンロード
- **matplotlib**: データ可視化
- **seaborn**: 統計グラフ作成

## ディレクトリ構成
```
book-recommender/
├── gradio-dashboard.py          # Gradioを用いたWebインターフェースのメインスクリプト
├── main.py                      # デフォルトのPythonスクリプト（未使用）
├── ReadMe.md                    # このREADMEファイル
├── chroma_books/                # ベクトルデータベースの保存ディレクトリ
│   └── chroma.sqlite3           # Chromaデータベースファイル
├── datasets/                    # データセットディレクトリ
│   ├── books_cleaned.csv        # クリーニング済みの書籍データ
│   ├── books_with_categories.csv # カテゴリ付き書籍データ
│   ├── books_with_emotions.csv  # 感情分析済み書籍データ
│   └── tagged_description.txt   # ISBNと説明文のタグ付きテキスト
└── processing_files/            # データ処理用のJupyterノートブック
    ├── data-exploration.ipynb   # データ探索と前処理
    ├── sentiment.ipynb          # 感情分析
    ├── text-classification.ipynb # テキスト分類（カテゴリ分類）
    └── vector-search.ipynb      # ベクトル検索の実装
```

## 各ファイルの内容
### gradio-dashboard.py
Gradioライブラリを使用して書籍推薦のWebインターフェースを作成するスクリプトです。ユーザーがクエリを入力し、カテゴリや感情を指定して書籍を推薦します。内部でベクトル検索と感情に基づくソートを行っています。

### main.py
PyCharmのデフォルトテンプレートスクリプトです。このプロジェクトでは使用していません。

### datasets/
- **books_cleaned.csv**: Kaggleからダウンロードした書籍データをクリーニングしたもの。欠損値の処理や基本的な前処理が施されています。
- **books_with_categories.csv**: 書籍にカテゴリ情報を追加したデータ。
- **books_with_emotions.csv**: 感情分析モデルを用いて、各書籍の説明文に感情（喜び、驚き、怒り、恐れ、悲しみ）の確率を付与したデータ。
- **tagged_description.txt**: ISBNと書籍の説明文を組み合わせたテキストファイル。ベクトルデータベースに登録するための形式です。

### processing_files/
- **data-exploration.ipynb**: データセットの探索と前処理を行うノートブック。欠損値の確認、相関係数の計算、データのクリーニングを行っています。
- **sentiment.ipynb**: 感情分析を行うノートブック。Transformerモデルを用いて書籍の説明文に感情を分類します。
- **text-classification.ipynb**: テキスト分類を行うノートブック。書籍のカテゴリ分類を実装しています。
- **vector-search.ipynb**: ベクトル検索の実装ノートブック。Chromaデータベースを使用した類似度検索をテストしています。

### chroma_books/
ベクトルデータベースChromaの保存場所。書籍の説明文をベクトル化して保存しています。

## 参考動画
このプロジェクトは、以下のYouTube動画を参考にして作成しました：
[書籍推薦システムの開発チュートリアル](https://www.youtube.com/watch?v=Q7mS1VHm3Yw&t=1s)

動画では、NLPとベクトル検索を用いた推薦システムの構築方法が詳しく解説されています。

## 使い方
1. 必要なライブラリをインストールしてください：
   ```
   pip install pandas numpy python-dotenv langchain langchain-openai langchain-chroma gradio rich kagglehub matplotlib seaborn
   ```

2. 環境変数ファイル(.env)を作成し、OpenAI APIキーを設定してください。

3. データセットをダウンロード：
   - processing_files/data-exploration.ipynbを実行してKaggleからデータを取得。

4. ベクトルデータベースを作成：
   - gradio-dashboard.pyを実行すると自動でChromaデータベースが作成されます。

5. アプリケーションを起動：
   ```
   python gradio-dashboard.py
   ```

6. Webブラウザで表示されるインターフェースから、書籍を検索・推薦できます。

## 注意事項
- OpenAI APIキーが必要です。API使用料が発生する可能性があります。
- データセットはKaggleからダウンロードするため、インターネット接続が必要です。
- 感情分析には事前学習済みモデルを使用しています。