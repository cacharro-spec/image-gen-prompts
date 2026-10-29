# Image Generation Prompts for ChatGPT

[日本語](#日本語) | [English](#english)

---

## 日本語

### 概要

ChatGPT の画像生成で使うプロンプトをまとめたワークスペースです。
加工したい画像とプロンプトを ChatGPT に貼り付けて依頼すると、プロンプトに沿って加工された画像が生成されます。

### 使い方

1. `pronpts/` から使いたいプロンプトファイル（`.md`）を開く
2. ChatGPT で新しいチャットを開く
3. 加工したい画像をアップロードする
4. プロンプトファイルの内容をすべてコピーして貼り付け、送信する
5. 生成された画像を確認し、必要に応じて「車の色をもっと濃く」などの追加指示で調整する

### ディレクトリ構成

```
image-gen-prompts/
├── README.md
└── pronpts/
    └── NEO- TOKYO/
        └── NEO-TOKYO-promts.md   # 車の写真の背景を近未来・東京のサイバーパンクな街に加工
```

テーマごとに `pronpts/` 配下にフォルダを作り、その中にプロンプトファイルを置きます。

### プロンプトの構成

各プロンプトファイルは次の 2 つで構成されています。

| 区分 | 内容 |
| --- | --- |
| 本文 | 生成したい画像の指示。目的、元画像で残すもの、背景・ライティング・構図・仕上がりなどを番号付きの項目で記述 |
| `--` 以降 | 避けたい要素のリスト（ネガティブプロンプト）。カンマ区切りで記述 |

ChatGPT にはネガティブプロンプト専用の入力欄がないため、`--` 以降も含めてファイル全体をそのまま貼り付けてください。

### 収録プロンプト

| テーマ | ファイル | 内容 |
| --- | --- | --- |
| NEO-TOKYO | [NEO-TOKYO-promts.md](pronpts/NEO-%20TOKYO/NEO-TOKYO-promts.md) | 写真の車の特徴（車種・色・アングル・カスタムなど）を読み取ってそのまま残し、背景を近未来東京（高架道路・ネオン・日本語の標識など）に置き換え、高級車の広告写真のように仕上げる。場所・天候・時間帯は元写真に合わせる（指定も可） |

#### 生成サンプル：NEO-TOKYO

![NEO-TOKYO 生成サンプル](pronpts/NEO-%20TOKYO/sample.png)

### どの車の写真でも使える

NEO-TOKYO のプロンプトは特定の車種向けではありません。最初にアップロードされた写真から車の特徴（車種、ボディタイプ、色、ライトやホイールの形、カスタムパーツ、撮影アングル）を判定させ、それらを変えずに背景とライティングだけを作り変えるよう指示しています。プロンプトを書き換えずに、そのまま貼り付けて使えます。

### 場所・天候・時間帯の決まり方（NEO-TOKYO）

指定しなければ、元写真から場所の種類（街中・高速道路・駐車場・山道・海沿いなど）、天候、時間帯を読み取り、それを近未来の NEO-TOKYO 風に作り変えます。昼の写真なら昼の NEO-TOKYO、雨の写真なら濡れた路面になります。

変えたい項目があるときは、プロンプトの後ろに 1 行足して送ります。指定した項目だけが変わり、残りは元写真に合わせます。

```
Location: waterfront bayshore expressway / Weather: after rain / Time of day: night
```

### プロンプトの追加方法

1. `pronpts/` 配下にテーマ名のフォルダを作る
2. プロンプトファイル（`.md`）を作成し、本文と `--` 以降のネガティブプロンプトを書く
3. この README の「収録プロンプト」表に 1 行追加する

---

## English

### Overview

This workspace collects prompts for ChatGPT image generation.
Paste the image you want to edit along with a prompt into ChatGPT, and it generates an image transformed according to the prompt.

### How to use

1. Open the prompt file (`.md`) you want to use under `pronpts/`
2. Start a new chat in ChatGPT
3. Upload the image you want to edit
4. Copy the entire contents of the prompt file, paste it, and send
5. Review the generated image and refine it with follow-up instructions if needed (e.g. "make the car color deeper")

### Directory structure

```
image-gen-prompts/
├── README.md
└── pronpts/
    └── NEO- TOKYO/
        └── NEO-TOKYO-promts.md   # Turns a car photo's background into a near-future Tokyo cyberpunk city
```

Each theme gets its own folder under `pronpts/`, containing its prompt file.

### Prompt structure

Each prompt file has two parts.

| Part | Contents |
| --- | --- |
| Main body | Instructions for the image to generate: the objective, what to keep from the original image, background, lighting, composition, and finish, written as numbered sections |
| After `--` | A comma-separated list of things to avoid (negative prompt) |

ChatGPT has no dedicated negative-prompt field, so paste the whole file as is, including the part after `--`.

### Prompts

| Theme | File | Description |
| --- | --- | --- |
| NEO-TOKYO | [NEO-TOKYO-promts.md](pronpts/NEO-%20TOKYO/NEO-TOKYO-promts.md) | Identifies the car's characteristics in the photo (model, color, viewpoint, modifications, etc.), keeps them unchanged, and replaces the background with a near-future Tokyo (elevated expressways, neon, Japanese signage, etc.), finished like a premium automotive ad photo. Location, weather, and time of day follow the original photo (or can be specified) |

#### Sample output: NEO-TOKYO

![NEO-TOKYO sample output](pronpts/NEO-%20TOKYO/sample.png)

### Works with any car photo

The NEO-TOKYO prompt is not tied to a specific car model. It first has ChatGPT identify the car's characteristics from the uploaded photo (model, body type, color, light and wheel design, aftermarket parts, camera viewpoint), then rebuilds only the background and lighting without changing them. Paste it as is; no edits needed.

### How location, weather, and time of day are chosen (NEO-TOKYO)

By default, the prompt reads the location type (city street, highway, parking lot, mountain road, coastal road, etc.), weather, and time of day from the original photo and reinterprets them as NEO-TOKYO. A daytime photo becomes a daytime NEO-TOKYO; a rainy photo gets a wet road.

To change any of them, add one line after the prompt. Only the items you specify change; the rest follow the original photo.

```
Location: waterfront bayshore expressway / Weather: after rain / Time of day: night
```

### Adding a prompt

1. Create a folder named after the theme under `pronpts/`
2. Create a prompt file (`.md`) with the main body and a negative prompt after `--`
3. Add a row to the "Prompts" table in this README
