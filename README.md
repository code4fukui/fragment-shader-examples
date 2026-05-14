# fragment-shader-examples

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A collection of examples demonstrating how to integrate GLSL fragment shaders into web pages using the `<fragment-shader>` custom HTML element.

## Demos

- **[Cloud](https://code4fukui.github.io/fragment-shader-examples/cloud.html)**: A full-screen, animated flight through volumetric clouds.
- **[Orb](https://code4fukui.github.io/fragment-shader-examples/orb.html)**: An interactive glowing orb that follows the mouse cursor.
- **[Multi-shader Page](https://code4fukui.github.io/fragment-shader-examples/)**: A single page showcasing three different shaders stacked vertically (Clouds, Julia Set, and Orb).

## Features

- **Multiple Effects**: Showcases visual effects like volumetric clouds, a dynamic Julia set fractal, and an interactive orb.
- **Simple Integration**: Uses the `<fragment-shader>` custom element, eliminating the need for complex WebGL boilerplate code.
- **Flexible Loading**: Demonstrates two ways to load shaders:
    1.  Embedding GLSL code directly inside the HTML tag.
    2.  Loading from an external `.glsl` file via the `src` attribute.
- **Interactive**: Examples use standard GLSL uniforms like `time`, `mouse`, and `resolution` to create animations and respond to user input.

## Usage

This project depends on the [`fragment-shader.js`](https://github.com/code4fukui/eggl/blob/main/fragment-shader.js) web component from the [eggl](https://github.com/code4fukui/eggl/) library.

To run the examples, simply open the HTML files in a web browser. To create your own, import the module and add the `<fragment-shader>` tag to your page.

### 1. Inline GLSL

You can write your shader code directly inside the `<fragment-shader>` tag. This is useful for small, self-contained effects.

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

### 2. External `.glsl` File

For more complex shaders, you can load them from an external file using the `src` attribute.

```html
<!-- From cloud.html -->
<script type="module" src="https://code4fukui.github.io/eggl/fragment-shader.js"></script>

<fragment-shader src="./cloud.glsl" fullscreen></fragment-shader>
```

## Acknowledgements

The shader effects in these examples are based on the work of others. Thank you to the original creators:

- **Cloud**: Based on [Dive to Cloud](https://www.shadertoy.com/view/ll3SWl) on Shadertoy.
- **Orb**: Based on [wgld.org | GLSL: オーブ(光の玉)のレンダリング](https://wgld.org/d/glsl/g003.html).
- **Julia Set**: Based on [wgld.org | GLSL: ジュリア集合](https://wgld.org/d/glsl/g006.html).

## License

This project is available under the [MIT License](LICENSE).