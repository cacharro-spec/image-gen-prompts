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

指定しなければ、元写真から場所の種類（街中・高速道路・駐車場・並木道・森の道・山道・海沿いなど）、天候、時間帯を読み取り、それを近未来の NEO-TOKYO 風に作り変えます。昼の写真なら昼の NEO-TOKYO、雨の写真なら濡れた路面になります。

- **天候**：雨にするのは、元写真に雨・濡れた路面・水たまり・車の水滴が写っているときだけです。晴れや曇りの写真では、車も路面も乾いたままにします。
- **時間帯**：空の明るさで判定します。街灯やヘッドライトが点いていても、空が明るければ昼か夕方として扱い、夜には変えません。ネオンが主役の雰囲気になるのは夜とブルーアワーだけです。
- **自然の中の道**：並木道・森・山・海沿い・田舎の道は、都市の道路に置き換えません。元の木々や景色を残したまま、道路を近未来の設備（埋め込み誘導灯、金属製のガードレール、未来的な街灯、東京方面の日本語標識）にし、道の先に NEO-TOKYO の街並みが霞んで見える「東京へ向かう道」にします。

変えたい項目があるときは、プロンプトの後ろに 1 行足して送ります。指定した項目だけが変わり、残りは元写真に合わせます。

```
Location: waterfront bayshore expressway / Weather: after rain / Time of day: night
```

### 傾いた写真の扱い（NEO-TOKYO）

カメラを傾けて撮った写真は、車と道路をまとめて回転させて水平に直します。回転や 16:9 への切り抜きで絵が足りなくなる部分（四隅や、縦長写真の左右）は、背景を自然に広げて埋めます。車の欠けた部分は作り足さず、車全体を画面に収めます。

車は必ず道路と同じ角度だけ回転させます。背景だけ水平にして車が元の傾きのまま残る、といったズレを防ぐため、元写真で「車の横方向の線（左右のライト・バンパー下端・ルーフ・左右タイヤの接地点）が路面と平行か」「車線のどこにいるか」を読み取り、生成後も同じ関係になっているかを最後にチェック項目（`9. FINAL CONSISTENCY CHECK`）で確認させています。

回転は車を 1 枚の写真のように丸ごと回す扱いにし、ルーフだけ水平でフロント面は傾いたまま、といった部分ごとの歪みを防ぎます。縦長写真を 16:9 にするときも車を横に引き伸ばさず、車の縦横比やライト・グリルの大きさは元写真のまま、増えた幅は背景で埋めます。

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

By default, the prompt reads the location type (city street, highway, parking lot, tree-lined avenue, forest road, mountain road, coastal road, etc.), weather, and time of day from the original photo and reinterprets them as NEO-TOKYO. A daytime photo becomes a daytime NEO-TOKYO; a rainy photo gets a wet road.

- **Weather**: rain is used only when the original photo shows rain, a wet road, puddles, or water drops on the car. Clear or cloudy photos keep the car and the road dry.
- **Time of day**: judged from the brightness of the sky. If the sky is bright, the scene stays daytime or dusk even when streetlights or headlights are on, and is never turned into night. The neon-dominated look is used only at night and blue hour.
- **Roads through nature**: tree-lined avenues and forest, mountain, coastal, or countryside roads are not replaced with city streets. The original trees and scenery are kept, the road becomes near-future infrastructure (embedded guide lights, metallic barriers, futuristic streetlights, Japanese signs pointing toward Tokyo), and the NEO-TOKYO skyline appears in the haze at the end of the road, like a road heading toward the city.

To change any of them, add one line after the prompt. Only the items you specify change; the rest follow the original photo.

```
Location: waterfront bayshore expressway / Weather: after rain / Time of day: night
```

### Tilted photos (NEO-TOKYO)

If the photo was taken with a tilted camera, the car and the road are rotated together to make the image level. Areas left without picture by the rotation or the 16:9 crop (corners, or the left and right sides of a vertical photo) are filled by naturally extending the background. Missing parts of the car are never invented, and the whole car is kept in the frame.

The car is always rotated by the same angle as the road. To prevent mismatches such as a leveled background with the car still tilted, the prompt reads from the original photo whether the car's crosswise lines (both lights, the bumper's bottom edge, the roof, and the left and right tire contact points) are parallel to the road surface and where the car sits in its lane, then has the model verify the same relationship in a final checklist (`9. FINAL CONSISTENCY CHECK`) before outputting the image.

The car is rotated as one rigid object, like rotating the photo itself, to prevent partial distortions such as a leveled roof with a front face that keeps the original slope. When a vertical photo becomes 16:9, the car is not stretched: its width-to-height ratio and the size of its lights and grille stay as in the original, and the extra width is filled with background.

### Adding a prompt

1. Create a folder named after the theme under `pronpts/`
2. Create a prompt file (`.md`) with the main body and a negative prompt after `--`
3. Add a row to the "Prompts" table in this README
