# WebGL: 2D and 3D graphics for the web

WebGL (Web Graphics Library) is a JavaScript API for rendering high-performance interactive 3D and 2D graphics  within any compatible web browser without the use of plug-ins. WebGL  does so by introducing an API that closely conforms to OpenGL ES 2.0  that can be used in HTML5 [`<canvas>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas) elements. This conformance makes it possible for the API to take advantage of  hardware graphics acceleration provided by the user's device.

Support for WebGL is present in [Firefox](https://developer.mozilla.org/en-US/Firefox) 4+, [Google Chrome](http://www.google.com/chrome/) 9+, [Opera](http://www.opera.com/) 12+, [Safari ](http://www.apple.com/safari/)5.1+, [Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/browser-ie) 11+, and [Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge) build 10240+; however, the user's device must also have hardware that supports these features.

The [WebGL 2](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API#WebGL_2) API introduces support for much of the OpenGL ES 3.0 feature set; it's provided through the [`WebGL2RenderingContext`](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext) interface.

The [`<canvas>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas) element is also used by the [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) to do 2D graphics on web pages.

## Reference

### Standard interfaces

- [`WebGLRenderingContext`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext)
- [`WebGL2RenderingContext`](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext)
- [`WebGLActiveInfo`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLActiveInfo)
- [`WebGLBuffer`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLBuffer)
- [`WebGLContextEvent`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLContextEvent)
- [`WebGLFramebuffer`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLFramebuffer)
- [`WebGLProgram`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLProgram)
- [`WebGLQuery`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLQuery)
- [`WebGLRenderbuffer`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderbuffer)
- [`WebGLSampler`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSampler)
- [`WebGLShader`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLShader)
- [`WebGLShaderPrecisionFormat`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLShaderPrecisionFormat)
- [`WebGLSync`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSync)
- [`WebGLTexture`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLTexture)
- [`WebGLTransformFeedback`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLTransformFeedback)
- [`WebGLUniformLocation`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLUniformLocation)
- [`WebGLVertexArrayObject`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLVertexArrayObject)

### Extensions

- [`ANGLE_instanced_arrays`](https://developer.mozilla.org/en-US/docs/Web/API/ANGLE_instanced_arrays)
- [`EXT_blend_minmax`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_blend_minmax)
- [`EXT_color_buffer_float`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_color_buffer_float)
- [`EXT_color_buffer_half_float`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_color_buffer_half_float)
- [`EXT_disjoint_timer_query`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_disjoint_timer_query)
- [`EXT_float_blend`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_float_blend)  
- [`EXT_frag_depth`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_frag_depth)
- [`EXT_sRGB`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_sRGB)
- [`EXT_shader_texture_lod`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_shader_texture_lod)
- [`EXT_texture_compression_bptc`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_texture_compression_bptc)
- [`EXT_texture_compression_rgtc`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_texture_compression_rgtc)
- [`EXT_texture_filter_anisotropic`](https://developer.mozilla.org/en-US/docs/Web/API/EXT_texture_filter_anisotropic)
- [`OES_element_index_uint`](https://developer.mozilla.org/en-US/docs/Web/API/OES_element_index_uint)
- [`OES_fbo_render_mipmap`](https://developer.mozilla.org/en-US/docs/Web/API/OES_fbo_render_mipmap)
- [`OES_standard_derivatives`](https://developer.mozilla.org/en-US/docs/Web/API/OES_standard_derivatives)
- [`OES_texture_float`](https://developer.mozilla.org/en-US/docs/Web/API/OES_texture_float)
- [`OES_texture_float_linear`](https://developer.mozilla.org/en-US/docs/Web/API/OES_texture_float_linear)
- [`OES_texture_half_float`](https://developer.mozilla.org/en-US/docs/Web/API/OES_texture_half_float)
- [`OES_texture_half_float_linear`](https://developer.mozilla.org/en-US/docs/Web/API/OES_texture_half_float_linear)
- [`OES_vertex_array_object`](https://developer.mozilla.org/en-US/docs/Web/API/OES_vertex_array_object)
- [`OVR_multiview2`](https://developer.mozilla.org/en-US/docs/Web/API/OVR_multiview2)
- [`WEBGL_color_buffer_float`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_color_buffer_float)
- [`WEBGL_compressed_texture_astc`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_astc)
- [`WEBGL_compressed_texture_atc`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_atc)
- [`WEBGL_compressed_texture_etc`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_etc)
- [`WEBGL_compressed_texture_etc1`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_etc1)
- [`WEBGL_compressed_texture_pvrtc`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_pvrtc)
- [`WEBGL_compressed_texture_s3tc`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_s3tc)
- [`WEBGL_compressed_texture_s3tc_srgb`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_s3tc_srgb)
- [`WEBGL_debug_renderer_info`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_debug_renderer_info)
- [`WEBGL_debug_shaders`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_debug_shaders)
- [`WEBGL_depth_texture`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_depth_texture)
- [`WEBGL_draw_buffers`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_draw_buffers)
- [`WEBGL_lose_context`](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_lose_context)

### Events

- `webglcontextlost`
- `webglcontextrestored`
- `webglcontextcreationerror`

### Constants and types

- [WebGL constants](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Constants)
- [WebGL types](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Types)

### WebGL 2

WebGL 2 is a major update to WebGL which is provided through the [`WebGL2RenderingContext`](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext) interface. It is based on OpenGL ES 3.0 and new features include:

- [3D textures](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/texImage3D),
- [Sampler objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSampler),
- [Uniform Buffer objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext#Uniform_buffer_objects),
- [Sync objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSync),
- [Query objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLQuery),
- [Transform Feedback objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLTransformFeedback),
- Promoted extensions that are now core to WebGL 2: [Vertex Array objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLVertexArrayObject), [instancing](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawArraysInstanced), [multiple render targets](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawBuffers), [fragment depth](https://developer.mozilla.org/en-US/docs/Web/API/EXT_frag_depth).

See also the blog post ["WebGL 2 lands in Firefox"](https://hacks.mozilla.org/2017/01/webgl-2-lands-in-firefox/) and [webglsamples.org/WebGL2Samples](http://webglsamples.org/WebGL2Samples/) for a few demos.

## Guides and tutorials

Below, you'll find an assortment of guides to help you learn WebGL  concepts and tutorials that offer step-by-step lessons and examples.

### Guides

- [Data in WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Data)

  A guide to variables, buffers, and other types of data used when writing WebGL code.

- [WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices)

  Tips and suggestions to help you improve the quality, performance, and reliability of your WebGL content.

- [Using extensions](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Using_Extensions)

  A guide to using WebGL extensions.

### Tutorials

- [WebGL tutorial](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Tutorial)

  A beginner's guide to WebGL core concepts. A good place to start if you don't have previous WebGL experience.

### Examples

- [A basic 2D WebGL animation example](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Basic_2D_animation_example)

  This example demonstrates the simple animation of a one-color  shape. Topics examined are adapting to aspect ratio differences, a  function to build shader programs from sets of multiple shaders, and the basics of drawing in WebGL.

- [WebGL by example](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/By_example)

  A series of live samples with short explanations that showcase  WebGL concepts and capabilities. The examples are sorted according to  topic and level of difficulty, covering the WebGL rendering context,  shader programming, textures, geometry, user interaction, and more.

### Advanced tutorials

- [WebGL model view projection](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_model_view_projection)

  A detailed explanation of the three core matrices that are  typically used to represent a 3D object view: the model, view and  projection matrices.

- [Matrix math for the web](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Matrix_math_for_the_web)

  A useful guide to how 3D transform matrices work, and can be used  on the web — both for WebGL calculations and in CSS3 transforms.

## Resources

- [Raw WebGL: An introduction to WebGL](https://www.youtube.com/embed/H4c8t6myAWU/?feature=player_detailpage) A talk by Nick Desaulniers that introduces the basics of WebGL. This is a great place to start if you've never done low-level graphics  programming.
- [Khronos WebGL site](http://www.khronos.org/webgl/) The main web site for WebGL at the Khronos Group.
- [WebGL Fundamentals](http://www.html5rocks.com/en/tutorials/webgl/webgl_fundamentals/) A basic tutorial with fundamentals of WebGL.
- [WebGL playground](http://webglplayground.net) An online tool for creating and sharing WebGL projects. Good for quick prototyping and experimenting.
- [WebGL Academy](http://www.webglacademy.com) An HTML/JavaScript editor with tutorials to learn basics of webgl programming.
- [WebGL Stats](http://webglstats.com/) A site with statistics about WebGL capabilities in browsers on different platforms.

### Libraries

- [glMatrix](https://github.com/toji/gl-matrix) is a JavaScript matrix and vector library for high-performance WebGL apps.
- [PhiloGL](http://senchalabs.github.com/philogl/) is a WebGL framework for data visualization, creative coding, and game development.
- [Pixi.js](http://www.pixijs.com/) is a fast, open-source 2D WebGL renderer.
- [PlayCanvas](https://playcanvas.com/) is an open-source game engine.
- [Sylvester](http://sylvester.jcoglan.com/) is an open-source library for manipulating vectors and matrices. Not optimized for WebGL but extremely robust.
- [three.js](https://threejs.org/) is an open-source, fully featured 3D WebGL library.
- [Phaser](https://phaser.io/) is a fast, free and fun open source framework for Canvas and WebGL powered browser games.
- [RedGL](https://github.com/redcamel/RedGL2) is an open-source 3D WebGL library.
- [vtk.js](https://kitware.github.io/vtk-js/) is a JavaScript library for scientific visualization in your browser.

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article17-folder/t1.jpg)

## Browser compatibility

### WebGL 1

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article17-folder/t2.jpg)

### WebGL 2

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article17-folder/t3.jpg)

### Compatibility notes

In addition to the browser, the GPU itself also needs to support the  feature. So, for example, S3 Texture Compression (S3TC) is only  available on Tegra-based tablets. Most browsers make the WebGL context  available through the `webgl` context name, but older ones need `experimental-webgl` as well. In addition, the upcoming [WebGL 2](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext) is fully backwards-compatible and will have the context name `webgl2`.

### Gecko notes

#### WebGL debugging and testing

Starting with Gecko 10.0 (Firefox 10.0 / Thunderbird 10.0 / SeaMonkey 2.7), there are two preferences available which let you control the  capabilities of WebGL for testing purposes:

- `webgl.min_capability_mode`

  A Boolean property that, when `true`, enables a minimum  capability mode. When in this mode, WebGL is configured to only support  the bare minimum feature set and capabilities required by the WebGL  specification. This lets you ensure that your WebGL code will work on  any device or browser, regardless of their capabilities. This is `false` by default.

- `webgl.disable_extensions`

  A Boolean property that, when `true`, disables all WebGL extensions. This is `false` by default.