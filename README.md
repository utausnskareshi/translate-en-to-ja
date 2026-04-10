# Google AI Edge Gallery カスタムスキル集

Google AI Edge Gallery（iPhone / Android アプリ）向けのカスタム Agent Skills リポジトリです。

---

## 収録スキル

| スキル名 | フォルダ | 概要 |
|---|---|---|
| 英語→日本語翻訳 | `translate-en-to-ja/` | 英語テキストを自然な日本語に翻訳する |

---

## スキルの詳細

### 英語→日本語翻訳（translate-en-to-ja）

英語で書かれたテキストを、文脈やニュアンスを保ちながら自然な日本語に翻訳します。

**特徴:**
- 日常会話・ビジネス文書・技術文書など幅広いジャンルに対応
- 原文のトーンや意図を維持した翻訳
- 日本語に対応する訳語がない技術用語は英語のまま残し、必要に応じて補足説明を付加
- 翻訳結果のみを出力（原文・解説・注釈は省略）

**GitHub Pages URL:**
```
https://utausnskareshi.github.io/translate-en-to-ja
```

---

## iPhoneアプリへの追加方法

### 前提条件

- [Google AI Edge Gallery](https://apps.apple.com/us/app/google-ai-edge-gallery/id6749645337) がインストール済みであること
- アプリ内でモデル（Gemma 4 など）がダウンロード済みであること

### 手順

1. アプリを起動し、ホーム画面から **「Agent Skills」** をタップする

2. チャット画面下部の **「Skills」** チップをタップして、Skill Manager を開く

3. 右上の **「＋」** ボタンをタップする

4. **「Load skill from URL」** を選択する

5. 以下の URL を入力し、**「Load」** をタップする
   ```
   https://utausnskareshi.github.io/translate-en-to-ja
   ```
   > **注意:** `https://` を省略すると App Transport Security（ATS）エラーが発生するため、必ず `https://` を含めて入力してください。

6. スキルが正常に読み込まれたことを確認し、**「Add」** をタップして追加完了

### スキルの使い方

スキルを追加後、Agent Skills のチャット画面で英語のテキストを含むメッセージを送ると、LLM が自動的にスキルを判断して翻訳を行います。

**入力例:**
```
Translate this: The weather is nice today.
```
```
Please translate the following sentence into Japanese: I would like to schedule a meeting for next Monday.
```

**出力例:**
```
今日はいい天気ですね。
```
```
来週の月曜日にミーティングを設定したいのですが。
```

---

## スキルのしくみ

本リポジトリのスキルは、Google AI Edge Gallery の **テキストオンリースキル** 形式で作成されています。

各スキルは `SKILL.md` ファイル 1 つで構成されており、以下の構造を持ちます。

```
translate-en-to-ja/
└── SKILL.md        ← スキル定義ファイル（フロントマター＋LLMへの指示）
```

`SKILL.md` の基本構造:

```markdown
---
name: スキル名（kebab-case）
description: スキルの概要（LLMがスキルを呼び出す判断に使用）
---

# スキルタイトル

## Instructions

LLMへの具体的な指示...
```

`description` フィールドはスキルの概要であると同時に、LLM がユーザーの入力内容と照合してスキルを自動起動するかどうかを判断するためのトリガー情報としても使われます。

---

## GitHub Pages の設定

本リポジトリは GitHub Pages を使ってスキルファイルを配信しています。

### 重要: `.nojekyll` ファイルについて

リポジトリルートに空の `.nojekyll` ファイルを配置しています。これにより GitHub Pages の Jekyll ビルドが無効化され、`SKILL.md` がそのままのテキストとして配信されます。このファイルがないと、Markdown ファイルが HTML に変換されてアプリからの読み込みに失敗します。

### 設定手順（新規リポジトリを作成する場合）

1. GitHub でリポジトリを作成し、スキルファイルを push する
2. **Settings → Pages → Source** で `Deploy from a branch` を選択
3. ブランチを `main`、フォルダを `/ (root)` に設定して **Save**
4. デプロイ完了後（数分かかる場合あり）、以下の URL で `SKILL.md` にアクセスできることを確認する
   ```
   https://<username>.github.io/<repository>/translate-en-to-ja/SKILL.md
   ```

---

## 参考リンク

- [Google AI Edge Gallery 公式リポジトリ](https://github.com/google-ai-edge/gallery)
- [スキル作成ガイド（README）](https://github.com/google-ai-edge/gallery/tree/main/skills)
- [Google AI Edge Gallery - App Store](https://apps.apple.com/us/app/google-ai-edge-gallery/id6749645337)
- [コミュニティスキル一覧（GitHub Discussions）](https://github.com/google-ai-edge/gallery/discussions/categories/skills)
