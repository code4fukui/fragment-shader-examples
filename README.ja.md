# fragment-shader-examples

`<fragment-shader>`カスタムHTML要素を使用して、GLSLフラグメントシェーダーをWebページに組み込む方法を示すサンプルのコレクションです。

## デモ

- **[Cloud](https://code4fukui.github.io/fragment-shader-examples/cloud.html)**: ボリュメトリッククラウド（体積雲）の中を飛行する、フルスクリーンのアニメーション。
- **[Orb](https://code4fukui.github.io/fragment-shader-examples/orb.html)**: マウスカーソルに追従する、インタラクティブに光るオーブ。
- **[Multi-shader Page](https://code4fukui.github.io/fragment-shader-examples/)**: 3つの異なるシェーダー（Cloud、Julia Set、Orb）を縦に並べて表示する単一ページ。

## 特徴

- **複数のエフェクト**: ボリュメトリッククラウド、動的なジュリア集合のフラクタル、インタラクティブなオーブなどの視覚効果を紹介します。
- **シンプルな組み込み**: `<fragment-shader>`カスタム要素を使用することで、複雑なWebGLのボイラープレートコード（定型コード）を不要にします。
- **柔軟な読み込み**: シェーダーの読み込み方法を2通り示します。
    1. HTMLタグ内にGLSLコードを直接埋め込む。
    2. `src`属性を使用して外部の`.glsl`ファイルから読み込む。
- **インタラクティブ**: `time`、`mouse`、`resolution`などの標準的なGLSLのuniform変数を使用して、アニメーションを作成し、ユーザーの入力に応答します。

## 使い方

このプロジェクトは、[eggl](https://github.com/code4fukui/eggl/)ライブラリの[`fragment-shader.js`](https://github.com/code4fukui/eggl/blob/main/fragment-shader.js) Webコンポーネントに依存しています。

サンプルを実行するには、HTMLファイルをWebブラウザで開くだけです。独自のものを作成するには、モジュールをインポートし、ページに`<fragment-shader>`タグを追加します。

### 1. インラインGLSL

シェーダーコードを直接`<fragment-shader>`タグ内に記述できます。これは、小規模で自己完結したエフェクトに便利です。

```html
<!-- From orb.html -->
<script type="module" src="https://code4fukui.github.io/eggl/fragment-shader.js"></script>

<fragment-shader>
#version 300 es
precision highp float;

uniform vec2  mouse;
uniform vec2  resolution;
out vec4 outColor;

void main(void) {
  vec2 m = vec2(mouse.x * 2.0 - 1.0, -mouse.y * 2.0 + 1.0);
  vec2 p = (gl_FragCoord.xy * 2.0 - resolution) / min(resolution.x, resolution.y);
  float t = 0.1 / length(m - p);
  outColor = vec4(vec3(t), 1.0);
}
</fragment-shader>
```

### 2. 外部`.glsl`ファイル

より複雑なシェーダーの場合は、`src`属性を使用して外部ファイルから読み込むことができます。

```html
<!-- From cloud.html -->
<script type="module" src="https://code4fukui.github.io/eggl/fragment-shader.js"></script>

<fragment-shader src="./cloud.glsl" fullscreen></fragment-shader>
```

## 謝辞

これらのサンプルにおけるシェーダーエフェクトは、他の方々の作品に基づいています。オリジナルの作成者に感謝いたします。

- **Cloud**: Shadertoyの[Dive to Cloud](https://www.shadertoy.com/view/ll3SWl)に基づいています。
- **Orb**: [wgld.org | GLSL: オーブ(光の玉)のレンダリング](https://wgld.org/d/glsl/g003.html)に基づいています。
- **Julia Set**: [wgld.org | GLSL: ジュリア集合](https://wgld.org/d/glsl/g006.html)に基づいています。

## ライセンス

このプロジェクトは[MIT License](LICENSE)の下で利用可能です。
