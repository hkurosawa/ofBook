<!--
Graphics
========
-->

# グラフィックス

<!--
*By: [Michael Hadley](http://www.mikewesthad.com/) with generous editor support from [Abraham Avnisan](http://abrahamavnisan.com/), [Brannon Dorsey](http://brannondorsey.com/) and [Christopher Baker](http://christopherbaker.net/).*
-->

_By: [Michael Hadley](http://www.mikewesthad.com/) with generous editor support from [Abraham Avnisan](http://abrahamavnisan.com/), [Brannon Dorsey](http://brannondorsey.com/) and [Christopher Baker](http://christopherbaker.net/)._

<!--
This chapter builds off of the _C++ Basics_ and _Setup and Project Structure_ chapters, so if you aren't familiar with basic C++ and creating openFrameworks projects, check out those chapters first.
-->

この章は _C++ Basics_ と _Setup and Project Structure_ の再構成なので、C++ の基礎と openFrameworks プロジェクトの作成に慣れていなければ、そちらの章をまずご覧ください。

<!--
In sections 1 and 2, we will create "paintbrushes" where the mouse is our brush and our code defines how our brush makes marks on the screen. In section 3, we will explore something called "coordinate system transformations" to create hypnotizing, spiraling rectangles. Source code for the projects is linked at the end of each section. If you feel lost at any point, don't hesitate to look at the completed code! You can check out the whole collection of code [here](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code) - both for standard development structure (Xcode, Code::Blocks, etc.) and for ofSketch.
-->

セクション 1 と 2 ではマウスがブラシとなりコードでブラシがどのように跡をつけるかを定義する「ペイントブラシ」を作成します。セクション 3 では、幻想的な螺旋状の四角形を作成するために「座標変換」と呼ばれるものについて見ていきます。プロジェクトのソースコードはそれぞれのセクションの最後にリンクされています。どこでも迷ったと感じたら、迷わず完全なコードに当たってください！[ここ](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code)からコードのコレクション全体をチェックアウトできます。一般的な開発環境（Xcode、Code::Blocks 等）と ofSketch 用があります。

<!--
If you are following along using ofSketch, great! There are a couple things to note. Coding in ofSketch is a bit different than coding in other Xcode, Code::Blocks, etc. 1) There will be a few points where variables are added to something called a header file (`.h`). When you see those instructions, that means you should put your variables above your `setup()` function in ofSketch. 2) You'll want to use `ofSetWindowShape(int width, int height)` in `setup()` to control the size of your application. 3) Some of the applications you write will save images to your computer. You can find them in your ofSketch folder, by looking for `ofSketch/data/Projects/YOUR_PROJECT_NAME/bin/data/`.
-->

もし ofSketch を使って進めようとしているなら、よろしい！いくつか注意点があります。ofSketch でコーディングするのは他の Xcode や Code::Blocks 等でコーディングするのとは少し異なります。1）ヘッダファイル（`.h`）と呼ばれるものに変数を追加する箇所が何箇所かあります。この指示を見たら、ofSketch では`setup()`関数の上に変数を追加することを意味します。2）`setup()`の中で`ofSetWindowShape(int width, int height)` を使ってアプリケーションのサイズを制御したくなるでしょう。3）いくつかのアプリケーションではコンピュータに画像を保存します。これらは ofSketch のフォルダの中の`ofSketch/data/Projects/YOUR_PROJECT_NAME/bin/data/`を探すことで見つかります。

<!--
## Brushes with Basic Shapes
-->

## 基本形状のブラシ

<!--
To create brushes, we need to define some basic building blocks of graphics. We can classify the 2D graphics functions into two categories: basic shapes and freeform shapes. Basic shapes are rectangles, circles, triangles and straight lines. Freeform shapes are polygons and paths. In this section, we will focus on the basic shapes.
-->

ブラシを作成するには、グラフィックスの基本的な構成要素を定義する必要があります。2D グラフィックス機能は 2 つのカテゴリに分類できます。それは、基本形状と自由形状です。基本形状は四角、円、三角形や直線です。自由形状はポリゴンやパスです。このセクションでは基本形状にフォーカスします。

<!--
### Basic Shapes
-->

### 基本形状

<!--
Before drawing any shape, we need to know how to specify locations on screen. Computer graphics use the [Cartesian coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system). Remember figure 1 (left) from math class? A pair of values `(x, y)` told us how far away we were from `(0, 0)`, the origin. Computer graphics are based on this same system, but with two twists. First, `(0, 0)` is the upper leftmost pixel of the screen. Second, the y axis is flipped such that the positive y direction is located below the origin figure 1 (center).
-->

何か形を描く前に、画面上の位置の指定方法を知っておきましょう。コンピュータグラフィックスは[デカルト座標系](https://ja.wikipedia.org/wiki/%E7%9B%B4%E4%BA%A4%E5%BA%A7%E6%A8%99%E7%B3%BB)を使っています。数学の授業での図 1 (左) を覚えていますか？`(x, y)`の値のペアがどれだけ`(0, 0)`つまり原点から離れているかを示しています。コンピュータグラフィックスはこの同じシステムを基礎としていますが、2 つの癖があります。一つ目は、`(0, 0)`が画面上左上隅のピクセルです。二つ目、y 軸が反転しているので、y の正の方向は図 1（中央）の原点からは下方向です。

<!--
If we apply this to the top left of my screen figure 1 (right), which happens to be my browser. We can see the pixels and identify their locations in our new coordinate system. The top left pixel is `(0, 0)`. The top left pixel of the blue calender icon (with the white "19") is `(58, 5)`.
-->

これを私のスクリーン、たまたまブラウザですが図 1（右）の左上に適用するとします。ピクセルを見ることができ、それらの位置を新しい座標系で特定することができます。左上のピクセルが`(0, 0)`です。青いカレンダーアイコン（白い"19"の数字が付いている）の左上のピクセルは`(58, 5)`です。

<!--
![Figure 1: 2D screen coordinates](images/Figure1_CoordSystemFigure.png)
-->

![図1: 2Dスクリーン座標系](images/Figure1_CoordSystemFigure.png)

<!--
Now that we can talk about locations, let's jump into code. Create an openFrameworks project and call it "BasicShapes" (or something more imaginative). Open the source file, `ofApp.cpp`, and navigate to the `draw()` function. Add the following:
-->

これで私たちは位置について語ることができますので、コードを見ていきましょう。openFrameworks のプロジェクトを作成して"BasicShapes"（またはもっと創造的なもの）と名付けます。`ofApp.cpp` のソースファイルを開き、`draw()`関数まで移動しましょう。以下を追加してください。

<!--
```cpp
ofBackground(0);  // Clear the screen with a black color
ofSetColor(255);  // Set the drawing color to white

// Draw some shapes
ofDrawRectangle(50, 50, 100, 100); // Top left corner at (50, 50), 100 wide x 100 high
ofDrawCircle(250, 100, 50); // Centered at (250, 100), radius of 50
ofDrawEllipse(400, 100, 80, 100); // Centered at (400 100), 80 wide x 100 high
ofDrawTriangle(500, 150, 550, 50, 600, 150); // Three corners: (500, 150), (550, 50), (600, 150)
ofDrawLine(700, 50, 700, 150); // Line from (700, 50) to (700, 150)
```
-->

```cpp
ofBackground(0);  // 黒で画面をクリアします
ofSetColor(255);  // 描画色を白に設定します

// 図形の描画
ofDrawRectangle(50, 50, 100, 100); // 左上が (50, 50), 幅100 x 高さ100
ofDrawCircle(250, 100, 50); // 中心点 (250, 100), 半径 50
ofDrawEllipse(400, 100, 80, 100); // 中心点 (400 100), 幅80 x 高さ100
ofDrawTriangle(500, 150, 550, 50, 600, 150); // 3つの角: (500, 150), (550, 50), (600, 150)
ofDrawLine(700, 50, 700, 150); // (700, 50) から (700, 150) までの直線
```

<!--
When we run the code, we see white shapes on a black background. Success! Each time our `draw()` function executes, three things happen. First, we clear the screen by drawing a solid black background using [`ofBackground(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofBackground). The `0` represents a grayscale color where `0` is completely black and `255` is completely white. Second, we specify what color should be used for drawing with [`ofSetColor(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetColor). We can think of this code as telling openFrameworks to pull out a specific colored marker. When we draw, we will draw in that color until we specify that we want another color. Third, we draw our basic shapes with [`ofDrawRectangle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawRectangle), [`ofDrawCircle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawCircle), [`ofDrawEllipse(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawEllipse), [`ofDrawTriangle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawTriangle) and [`ofDrawLine(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawLine). Check out the comments in the example to better understand how we are using the drawing functions. The functions can be used in other ways as well, so check out the openFrameworks documentation if you are curious.
-->

コードを実行すると、黒色の背景に白い図形が現れます。成功です！`draw()`関数が実行される度に 3 つの事柄が起こります。まず、[`ofBackground(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofBackground)によって黒の単色で画面を消去します。`0`はグレースケールで、`0`は真っ黒、`255`は真っ白を表します。2 番目に、[`ofSetColor(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetColor)で描画時に何色を使うかを指定します。このコードは openFrameworks に特定のカラーマーカーを取り出させるものと考えることができます。描画の際には、他の色にしたいと指定するまではこの色で描画されます。3 番目に、[`ofDrawRectangle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawRectangle), [`ofDrawCircle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawCircle), [`ofDrawEllipse(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawEllipse), [`ofDrawTriangle(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawTriangle) and [`ofDrawLine(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawLine)で基本形状を描画します。描画の関数をどのように利用しているかをより詳しく知るには、サンプルのコメントを確認してください。これらの関数は別の使い方もできますので、興味があれば openFrameworks のドキュメントにも当たってください。

<!--
[`ofFill()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofFill) and [`ofNoFill()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofFill) toggle between drawing filled shapes and drawing outlines. The colored marker analogy doesn't fit, but the concept still applies. `ofFill()` tells openFrameworks to draw filled shapes until told otherwise. `ofNoFill()` does the same but with outlines. So we can draw two rows of shapes on our screen (figure 2) - one filled and one outlines - if we modify our `draw()` function to look like:
-->

[`ofFill()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofFill) と [`ofNoFill()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofFill) は塗りつぶしの形状と輪郭の描画を切り替えます。カラーマーカーの例えはうまく当てはまりませんが、それでも概念は使えます。`ofFill`は openFrameworks に対して、別のものを命令するまで塗りつぶしの形状を描画するように伝えます。`ofNoFill()`は輪郭に対して同様のことを行います。したがって私たちは、`draw()`関数を下記のように変更すれば、2 行に渡る形状、一つは塗りつぶしでもう一つは輪郭線を、画面上（図 2）に描画します。

<!--
```cpp
ofFill(); // If we omit this and leave ofNoFill(), all the shapes will be outlines!
// Draw some shapes (code omitted)

ofNoFill(); // If we omit this and leave ofFill(), all the shapes will be filled!
// Draw some shapes (code omitted)
```
-->

```cpp
ofFill(); // これを消してofNoFill()を残せば、全ての形状が輪郭線になります！
// 図形を描画する (コードは省略)

ofNoFill(); // これを消してofFill()を残せば、全ての形状が塗りつぶしになります！
// 図形を描画する (コードは省略)
```

<!--
The circle and ellipse are looking a bit jagged, so we can fix that with [`ofSetCircleResolution(...)`](http://openframeworks.cc/documentation/gl/ofGLProgrammableRenderer.html#!show_setCircleResolution). Circles and ellipses are drawn by connecting a series of points with straight lines. If we take a close look at the circle in figure 2, and we'll be able to identify the 20 tiny straight lines. That's the default resolution. Try putting `ofSetCircleResolution(50)` in the `setup()` function.
-->

円および楕円形がいささかギザギザに見えるので、[`ofSetCircleResolution(...)`](http://openframeworks.cc/documentation/gl/ofGLProgrammableRenderer.html#!show_setCircleResolution)でこれを修正しましょう。円や楕円は点の連なりを直線で繋げることによって描画しています。図 2 の円を良く見てみると、20 個の小さな直線を見つけることができます。これがデフォルトの解像度です。`setup()`関数の中に`ofSetCircleResolution(50)`を書いてみてください。

<!--
The individual lines that make up our outlines can be jagged too. We can fix that with a smoothing technique called [anti-aliasing](https://en.wikipedia.org/wiki/Spatial_anti-aliasing). We probably don't need to worry about this since anti-aliasing will be turned on by default in recent versions of openFrameworks. If it isn't, just add [`ofEnableAntiAliasing()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEnableAntiAliasing) to `setup()`. (For future reference, you can turn it off to save computing power: [`ofDisableAntiAliasing()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofDisableAntiAliasing).)
-->

輪郭を形成している個々の直線もギザついているかもしれません。これは[アンチエイリアシング](https://en.wikipedia.org/wiki/Spatial_anti-aliasing)というスムージングのテクニックで修正できます。アンチエイリアシングは openFrameworks の最近のバージョンではデフォルトで有効になっているので恐らくこれを心配する必要はありません。もしそうでなければ、単に`setup()`に[`ofEnableAntiAliasing()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEnableAntiAliasing)を追加してください。 (今後のために、計算パワーの節約のために無効化もできます: [`ofDisableAntiAliasing()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofDisableAntiAliasing)）

<!--
![Figure 2: Basic shapes with and without a fill](images/Figure2_BasicShapes.png)
-->

![図2: 塗りつぶし有りと無しの基本形状](images/Figure2_BasicShapes.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_i_Basic_Shapes)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_i_Basic_Shapes.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_i_Basic_Shapes)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_i_Basic_Shapes.sketch)\]

<!--
**Extensions**
-->

**拡張**

<!--
1. We can change the thickness of lines using [`ofSetLineWidth(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetLineWidth). The default thickness is 1. We use this function like `ofFill()` and `ofSetColor(...)` in that it changes the thickness of the "marker" we use to draw lines. Note: the range of widths supported by this feature is dependent on your graphics card, so if it's not working, it might not be your fault!
2. Draw some rounded rectangles using [`ofDrawRectRounded(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawRectRounded)\.
3. Explore the world of curved lines with [`ofDrawCurve(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawCurve) and [`ofDrawBezier(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawBezier). You can control the resolution using [`ofSetCurveResolution(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofSetCurveResolution)\.
-->

1. 線の太さは[`ofSetLineWidth(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetLineWidth)で変更できます。デフォルトの太さは 1 です。1. この関数は`ofFill()`や`ofSetColor(...)`のように線を描画する際の「マーカー」の太さを変更するために利用します。注意：この機能のサポートされる線幅の範囲はグラフィックスカードに依存しますので、もし動作しなくてもたぶんあなたのせいではありませんよ！
2. [`ofDrawRectRounded(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawRectRounded)で角丸を描画してみましょう。
3. Explore the world of curved lines with [`ofDrawCurve(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawCurve)や[`ofDrawBezier(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofDrawBezier)で曲線の世界を探索してみましょう。解像度は[`ofSetCurveResolution(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofSetCurveResolution)で調整できます。

<!--
### Brushes from Basic Shapes
-->

### 基本形状からのブラシ

<!--
We survived the boring bits, but why draw one rectangle, when we can draw a million (figure 3)? That is essentially what we will be doing in this section. We will build brushes that drop a burst of many small shapes whenever we press the left mouse button. To make things more exciting, we will mix in some randomness. Start a new openFrameworks project, called "ShapeBrush."
-->

退屈な部分はなんとかクリアしましたが、百万もの四角形を描く（図 3）ことが可能なのに、なんで一つだけ描画しているんでしょう？これが本質的にはこのセクションにおいて行っていくことです。左マウスボタンを押下するとたくさんの小さな形状を散らしていくようなブラシを作っていきましょう。もっと面白くするために、いくらかランダム性も取り入れます。新規の openFrameworks プロジェクトを開始して、"ShapeBrush" と名付けましょう。

<!--
![Figure 3: Okay, not actually a million rectangles](images/Figure3_LotsOfRectangles.png)
-->

![図3: オーケー、本当は百万個はないですよ](images/Figure3_LotsOfRectangles.png)

<!--
#### Single Rectangle Brush: Using the Mouse
-->

#### 単一の四角形のブラシ：マウスの利用

<!--
We are going to lay down the foundation for our brushes by making a simple one that draws a single rectangle when we hold down the mouse. To get started, we are going to need to know 1) the mouse location and 2) if the left mouse button is pressed.
-->

マウスを押下した際に一つの四角形を描画するようなシンプルなものを作成して、ブラシの基礎を作っていきましょう。はじめに、1）マウスの位置、そして 2）左マウスボタンが押されたかどうか、を知る必要があります。

<!--
For 1), we can use two openFrameworks functions that return `int` variables: [`ofGetMouseX()`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMouseX) and [`ofGetMouseY()`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMouseY). We will use them in `draw()`.
-->

1）については、[`ofGetMouseX()`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMouseX) と [`ofGetMouseY()`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMouseY) という`int`h 連数を返す 2 つの openFrameworks の関数が使えます。これらは`draw()`の中で使いましょう。

<!--
For 2), we can find out whether the left mouse button is pressed using [`ofGetMousePressed(...)`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMousePressedd). The function asks us to pass in an `int` that represents which mouse button is we want to know about. openFrameworks provides some "public constants" for use here: `OF_MOUSE_BUTTON_LEFT`, `OF_MOUSE_BUTTON_MIDDLE` and `OF_MOUSE_BUTTON_RIGHT`. These public constants are just `int` variables that cannot be changed and can be accessed anywhere you have included openFrameworks. So `ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)` will return `true` if the left button is pressed and will return `false` otherwise.
-->

2）については、[`ofGetMousePressed(...)`](http://openframeworks.cc/documentation/events/ofEvents.html#show_ofGetMousePressedd)を使って左マウスボタンが押されたかどうかを知ることができます。この関数には、私たちが知りたいのはどのマウスボタンが押されたかを示す`int`を渡す必要があります。openFrameworks はここで利用できるいくつかの「パブリック定数」、`OF_MOUSE_BUTTON_LEFT`、`OF_MOUSE_BUTTON_MIDDLE`そして`OF_MOUSE_BUTTON_RIGHT`といったものを提供しています。これらのパブリック定数は変更が不可能かつ openFrameworks を組み込んでいればどこからでもアクセスが可能な、単なる`int`の変数です。したがって、`ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)`は左マウスボタンが押下されていれば`true`を返しますし、そうでなければ`false`を返却します。

<!--
Let's add some graphics. Hop over to the `draw()` function where we can bring these new functions together:
-->

グラフィックスを追加してみましょう。`draw()`関数に行って、これらの新しい関数を組み合わせてみましょう。

<!--
```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)) {  // If the left mouse button is pressed...
    ofSetColor(255);
    ofSetRectMode(OF_RECTMODE_CENTER);
    ofDrawRectangle(ofGetMouseX(), ofGetMouseY(), 50, 50);  // Draw a 50 x 50 rect centered over the mouse
}
```
-->

```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)) {  // 左マウスボタンが押されたら…
    ofSetColor(255);
    ofSetRectMode(OF_RECTMODE_CENTER);
    ofDrawRectangle(ofGetMouseX(), ofGetMouseY(), 50, 50);  // マウスを中心に50 x 50の四角形を描画
}
```

<!--
[`ofSetRectMode(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetRectMode) allows us to control how the `(x, y)` we pass into `ofDrawRectangle(...)` are used to draw. By default, they are interpreted as the upper left corner (`OF_RECTMODE_CORNER`). For our purposes, we want them to be the center (`OF_RECTMODE_CENTER`), so our rectangle is centered over the mouse.
-->

[`ofSetRectMode(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetRectMode) で私たちが`ofDrawRectanble(...)`に渡した `(x, y)` を描画にどのように利用するかを制御できます。デフォルトでは、これらは左上隅（`OF_RECTMODE_CORNER`）と解釈されます。私たちの目的としては、四角形はマウスが中央に来るようにしたいのでこれは中心点（`OF_RECTMODE_CENTER`）であってほしいです。

<!--
Compile and run. A white rectangle is drawn at the mouse position when we press the left mouse button ... but it disappears immediately. By default, the screen is cleared with every `draw()` call. We can change that with [`ofSetBackgroundAuto(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetBackgroundAuto). Passing in a value of `false` turns off the automatic background clearing. Add the following lines into `setup()`:
-->

コンパイルと実行をしましょう。左マウスボタンを押下するとマウスの一に白い四角形が描画されますね…しかしすぐに消えてしまいます。デフォルトでは、画面は毎回`draw()`の度にクリアされてしまいます。これは[`ofSetBackgroundAuto(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofSetBackgroundAuto)で変更ができます。`false`を値として渡すと自動的に背景がクリアされることをオフにできます。`setup()`に以下の行を追加しましょう。

<!--
```cpp
ofSetBackgroundAuto(false);

// We still want to draw on a black background, so we need to draw
// the background before we do anything with the brush
ofBackground(0);
```
-->

```cpp
ofSetBackgroundAuto(false);

// 黒い背景の上には描画したいので、
// ブラシで何かを行う前に背景を描画する必要はあります。
ofBackground(0);
```

<!--
First brush, done! We are going to make this a bit more interesting by adding 1) randomness and 2) repetition.
-->

最初のブラシは、完成です！これから 1）ランダム性と 2）繰り返しを追加することでもっと興味深いものにしていきましょう。

<!--
Randomness can make our code dark, mysterious and unpredictable. Meet [`ofRandom(...)`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofRandom). It can be used in two different ways: by passing in two values `ofRandom(float min, float max)` or by passing in a single value `ofRandom(float max)` where the min is assumed to be `0`. The function returns a random value between the min and max. We can inject some randomness into our rectangle color (figure 4) by using:
-->

ランダム性は私たちのコードを暗く、ミステリアスで予測不能にします。[`ofRandom(...)`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofRandom)を見てみましょう。これは 2 種類の方法で利用でき、`ofRandom(float min, float max)` または一つの値を `ofRandom(float max)` のように渡して、これは min が`0`であるとみなされます。

<!--
```cpp
float randomColor = ofRandom(50, 255);
ofSetColor(randomColor);  // Exclude dark grayscale values (0 - 50) that won't show on black background
```
-->

```cpp
float randomColor = ofRandom(50, 255);
ofSetColor(randomColor);  // 暗いグレーの値 (0 - 50) は黒い背景で見えないので除外します
```

<!--
![Figure 4: Drawing a rectangle snake](images/Figure4_RectangleSnake.png)
-->

![図4: 四角形の蛇を描く](images/Figure4_RectangleSnake.png)

<!--
To finish off this single rectangle brush, let's add the ability to erase by pressing the right mouse button by adding this to our `draw()` function:
-->

この単一の四角形によるブラシを完成させるために、以下を`draw()`関数に追加して右クリックをすると消去できる機能を加えましょう。

<!--
```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_RIGHT)) {  // If the right mouse button is pressed...
    ofBackground(0);  // Draw a black background over the screen
}
```
-->

```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_RIGHT)) {  // 右マウスボタンが押下されたら…
    ofBackground(0);  // 画面いっぱいに黒い背景を描画します。
}
```

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush.sketch)\]

<!--
#### Bursting Rectangle Brush: Creating Randomized Bursts
-->

#### 四角形が飛び散るブラシ：ランダムな飛散を作る

<!--
We now have the basics in place for a brush, but instead of drawing a single rectangle in `draw()`, let's draw a burst of randomized rectangles. We are going use a `for` loop to create multiple rectangles whose parameters are randomly chosen. What can we randomize? Grayscale color, width and height are easy candidates. We can also use a small positive or negative value to offset each rectangle from mouse position. Modify `draw()` to look like this:
-->

ブラシの基礎はできましたが、`draw()`の中で単一の四角形を描画する代わりに、ランダムな四角形が飛び散るのを描画してみましょう。`for`ループを使って複数の四角形を作成し、そのパラメータはランダムに選択されるようにします。なにがランダムにできるでしょう？グレースケールの色、幅や高さが単純な候補になるでしょう。わずかな正負の値でそれぞれの四角形をマウス位置からオフセットすることもできます。`draw()`を以下のように改変しましょう。

<!--
```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)) {  // If the left mouse button is pressed...
    ofSetRectMode(OF_RECTMODE_CENTER);
    int numRects = 10;
    for (int r=0; r<numRects; r++) {
        ofSetColor(ofRandom(50, 255));
        float width = ofRandom(5, 20);
        float height = ofRandom(5, 20);
        float xOffset = ofRandom(-40, 40);
        float yOffset = ofRandom(-40, 40);
        ofDrawRectangle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, width, height);
    }
}
```
-->

```cpp
if (ofGetMousePressed(OF_MOUSE_BUTTON_LEFT)) {  // 左マウスボタンが押されると…
    ofSetRectMode(OF_RECTMODE_CENTER);
    int numRects = 10;
    for (int r=0; r<numRects; r++) {
        ofSetColor(ofRandom(50, 255));
        float width = ofRandom(5, 20);
        float height = ofRandom(5, 20);
        float xOffset = ofRandom(-40, 40);
        float yOffset = ofRandom(-40, 40);
        ofDrawRectangle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, width, height);
    }
}
```

<!--
But! Add one more thing, inside of `setup()`, before hitting run: `ofSetFrameRate(60)`. The frame rate is the speed limit of our program, frames per second (fps). `update()` and `draw()` will not run more than `60` times per second. (ofSketch users - we'll talk about `update()` later.) Note: this is a speed _limit_, not a speed _minimum_ - our code can run slower than `60` fps. We set the frame rate in order to control how many rectangles will be drawn. If `10` rectangles are drawn with the mouse pressed and we know `draw()` won't be called more than `60` times per second, then we will generate a max of `600` rectangles per second.
-->

しかし！実行ボタンを押す前に、`setup()`の中にもう一つ、`ofSetFrameRate(60)`を追加してください。フレームレートはプログラムの速度制限で、１秒あたりのフレーム数（fps）です。`update()`と`draw()`は秒あたり`60`回以上は実行されません。（ofSketch ユーザの皆さん、`update()`については後ほどお話します）注意。これは速度の _制限_ であって、_最低_ の速度ではありません。コードは`60`fps よりも遅く動作することがあります。いくつの四角形が描画されるかを制御するためにフレームレートを設定しました。マウスを押下すると`10`個の四角形が描画されるとして`draw()`は`60`回以上は 1 秒あたりに呼ばれないので、1 秒あたり最大`600`個の四角形が生成されることになります。

<!--
Compile, run. We get a box-shaped spread of random rectangles (figure 5, left). Why didn't we get a circular spread (figure 5, right)? Since `xOffset` and `yOffset` could be any value between `-40` and `40`, think about what happens when `xOffset` and `yOffset` take on their most extreme values, i.e. (xOffset, yOffset) values of (-40, -40), (40, -40), (40, 40) and (-40, 40).
-->

コンパイル、実行しましょう。ランダムな四角形が箱型に広がります（図 5、左）どうして円形（図 5、右）に広がらないのでしょう？`xOffset`と`yOffset`は`-40`と`40`の間のどのような値でも取りうるので、`xOffset`と`yOffset`が最大の値を取ったとき、つまり(xOffset, yOffset)が(-40, -40)、(40, -40)、(40, 40)そして(-40, 40)の値になったときに何が起きるかを考えてみてください。

<!--
If we want a random point within a circle, it helps to think in terms of angles. Imagine we are at the center of a circle. If we rotate a random amount (the _polar angle_) and then move a random distance (the _polar radius_), we end up in a random location within the circle (assuming we don't walk so far that we cross the boundary of our circle). We just defined a point by a polar angle and a polar radius instead of using `(x, y)`. We have just thought about space in terms of [Polar coordinates](https://en.wikipedia.org/wiki/Polar_coordinate_system), instead of [Cartesian coordinates](https://en.wikipedia.org/wiki/Cartesian_coordinate_system).
-->

ランダムな点を円の中に収めたければ、角度で考えると良いです。私たちは円の中心にいると想像してください。ランダムな角度（_極角_）だけ回転して、その後ランダムな距離（_極距離_）だけ移動すると、私たちは円の中のランダムな位置にたどり着きます（円の境界を超えるほど遠くには行かないとします）。私たちは単に、`(x, y)`を使う代わりに極角と極距離を使用して点を指定しただけです。空間を[デカルト座標系](https://ja.wikipedia.org/wiki/%E7%9B%B4%E4%BA%A4%E5%BA%A7%E6%A8%99%E7%B3%BB)ではなく[極座標系](https://ja.wikipedia.org/wiki/%E6%A5%B5%E5%BA%A7%E6%A8%99%E7%B3%BB)によって捉えてみることをやってみました。

<!--
Back to the code. When we figure out our offsets, we want to pick a random direction (polar angle) and random distance (polar distance) which we can then convert to Cartesian coordinates (see code) to use as `xOffset` and `yOffset`. Our loop inside of `draw()` will look like this:
-->

コードに戻りましょう。オフセットを理解したところで、ランダムな方向（極角）およびランダムな距離（極距離）を選び、デカルト座標系（コードを見てください）に変換して`xOffset`および`yOffset`として使用しましょう。`draw()`の中のループはこんな風になります。

<!--
```cpp
for (int r=0; r<numRects; r++) {
    ofSetColor(ofRandom(50, 255));
    float width = ofRandom(5, 20);
    float height = ofRandom(5, 20);
    float distance = ofRandom(35);

    // Formula for converting from polar to Cartesian coordinates:
    //  x = cos(polar angle) * (polar distance)
    //  y = sin(polar angle) * (polar distance)

    // We need our angle to be in radians if we want to use sin() or cos()
    // so we can make use of an openFrameworks function to convert from degrees
    // to radians
    float angle = ofRandom(ofDegToRad(360.0));

    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    ofDrawRectangle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, width, height);
}
```
-->

```cpp
for (int r=0; r<numRects; r++) {
    ofSetColor(ofRandom(50, 255));
    float width = ofRandom(5, 20);
    float height = ofRandom(5, 20);
    float distance = ofRandom(35);

    // 極座標からデカルト座標への変換公式
    //  x = cos(polar angle) * (polar distance)
    //  y = sin(polar angle) * (polar distance)

    // sin()やcos()を使う場合には角度はラジアンである必要がある
    // 角度からラジアンへの変換には
    // openFrameworksの関数が使えます
    float angle = ofRandom(ofDegToRad(360.0));

    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    ofDrawRectangle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, width, height);
}
```

<!--
![Figure 5: Cartesian brush spread versus polar brush spread](images/Figure5_CartesianVsPolarSpread.png)
-->

![図5: デカルド座標系による拡散と極座標系による拡散](images/Figure5_CartesianVsPolarSpread.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_b_Bursting_Rect_Brush)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_b_Bursting_Rect_Brush)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_a_Single_Rectangle_Brush.sketch)\]

<!--
#### Glowing Circle Brush: Using Transparency and Color
-->

#### 光彩を放つ円形のブラシ：透明度と色を使用する

<!--
Unlike what we did with the rectangle brush, we are going to layer colorful, transparent circles on top of each to create a glowing haze. We will draw a giant transparent circle, then draw a slightly smaller transparent circle on top of it, then repeat, repeat, repeat. We can add transparency to `ofSetColor(...)` with a second parameter, the alpha channel (e.g.`ofSetColor(255, 50)`), with a value from `0` (completely transparent) to `255` (completely opaque).
-->

四角形のブラシでやったこととは異なり、カラフルで透明な円を上に重ねて行き、輝く煙のようにしてみましょう。巨大で透明な円を描画し、次に少し小さな透明の円をその上に、そして繰り返し、繰り返し、繰り返します。透明度は`ofSetColor(...)`の 2 つ目のパラメタ、アルファチャンネルで追加でき（例 `ofSetColor(255, 50)`）、この値は`0`（完全に透明）から`255`（完全に不透明）です。。

<!--
Before we use alpha, we need to enable something called "alpha blending." Using transparency costs computing power, so [`ofEnableAlphaBlending()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEnableAlphaBlending) and [`ofDisableAlphaBlending()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofDisableAlphaBlending) allow us to turn on and off this blending at our discretion. We need it, so enable it in `setup()`.
-->

アルファ値を使う前に、「アルファブレンディング」というものを有効にする必要があります。透明度を扱うことは計算のパワーを使うので、[`ofEnableAlphaBlending()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEnableAlphaBlending) そして [`ofDisableAlphaBlending()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofDisableAlphaBlending) を使って私たちの判断によるオン・オフが可能です。私たちには必要ですので、`setup()`の中で有効化しましょう。

<!--
Comment out the rectangle brush code inside the `if` statement that checks if the left mouse button is pressed. Now we can start working on our circle brush. We will use the `angle`, `distance`, `xOffset` and `yOffset` code like before. Our `for` loop will start with a large radius and step its value to `0`. Add the following:
-->

左マウスボタンが押されたかどうかを判断している`if`宣言の中の四角形のブラシのコードはコメントアウトしましょう。これで円形のブラシに取りかかれます。`angle`、`distance`、`xOffset`と`yOffset`のコードを前と同じように使って行きます。`for`ループは大きな半径から始まって`0`まで段階的に進みます。以下を追加しましょう。

<!--
```cpp
int maxRadius = 100;  // Increase for a wider brush
int radiusStepSize = 5;  // Decrease for more circles (i.e. a more opaque brush)
int alpha = 3;  // Increase for a more opaque brush
int maxOffsetDistance = 100;  // Increase for a larger spread of circles
// draw smaller and smaller circles and layering (increasing) opaqueness
for (int radius=maxRadius; radius>0; radius-=radiusStepSize) {
    float angle = ofRandom(ofDegToRad(360.0));
    float distance = ofRandom(maxOffsetDistance);
    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    ofSetColor(255, alpha);
    ofDrawCircle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, radius);
}
```
-->

```cpp
int maxRadius = 100;  // 太いブラシにするには大きくします
int radiusStepSize = 5;  // 小さくするとより多くの円を描きます（つまりより不透明になる）
int alpha = 3;  // 大きくすると不透明度が上がります。
int maxOffsetDistance = 100;  // 大きくすると円が広く拡散します
// だんだん小さくなる円を描いて不透明度を重ねて（高めて）いきます
for (int radius=maxRadius; radius>0; radius-=radiusStepSize) {
    float angle = ofRandom(ofDegToRad(360.0));
    float distance = ofRandom(maxOffsetDistance);
    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    ofSetColor(255, alpha);
    ofDrawCircle(ofGetMouseX()+xOffset, ofGetMouseY()+yOffset, radius);
}
```

<!--
![Figure 6: Results of using the circle glow brush](images/Figure6_CircleGlowBrush.png)
-->

![図6: 輝く円形のブラシを使用した結果](images/Figure6_CircleGlowBrush.png)

<!--
We end up with something like figure 6, a glowing light except without color. Tired of living in moody shades of gray? `ofSetColor(...)` can make use of the [Red Blue Green (RGB) color model](https://en.wikipedia.org/wiki/RGB_color_model) in addition to the grayscale color model. We specify the amount (`0` to `255`) of red, blue and green light respectively, e.g. `ofSetColor(255, 0, 0)` for opaque red. We can also add alpha, e.g. `ofSetColor(0, 0, 255, 10)` for transparent blue. Go ahead and modify the `ofSetColor(...)` in our circle brush to use a nice orange: `ofSetColor(255, 103, 0, alpha)`.
-->

図 6 みたいな光るライトのような感じの、色無しのものになりました。物憂げなグレー色の生活には飽き飽きでしょうか？`ofSetColor(...)`はグレースケールのカラーモデルに加えて[Red Blue Green (RGB) カラーモデル](https://en.wikipedia.org/wiki/RGB_color_model)が使えます。赤、青と緑の光の量（`0`から`255`）をそれぞれ、`ofSetColor(255, 0, 0)`のように指定します。アルファ値も加えることができ、例えば透明な青は`ofSetColor(0, 0, 255, 10)`になります。円形ブラシの`ofSetColor(...)`を変更して良い感じのオレンジ、`ofSetColor(255, 103, 0, alpha)`にしましょう。

<!--
There's another way we can use `ofSetColor(...)`. Meet [`ofColor`](http://openframeworks.cc/documentation/types/ofColor.html), a handy class for handling colors which allows for fancy color math (among other things). Here are some examples of defining and modifying colors:
-->

`ofSetColor(...)`を使う別の方法もあります。高度な色の計算（それと他の事も）が可能で色を扱うのに便利なクラスである[`ofColor`](http://openframeworks.cc/documentation/types/ofColor.html)を見てみましょう。色の定義や調整の例をいくつか示します。

<!--
```cpp
ofColor myOrange(255, 132, 0); // Defining an opaque orange color - specified using RGB
ofColor myBlue(0, 0, 255, 50); // Defining a transparent blue color - specified using RGBA

// We can access the red, green, blue and alpha channels like this:
ofColor myGreen(0, 0, 255, 255);
cout << "Red channel:" << myGreen.r << endl;
cout << "Green channel:" << myGreen.g << endl;
cout << "Blue channel:" << myGreen.b << endl;
cout << "Alpha channel:" << myGreen.a << endl;

// We can also set the red, green, blue and alpha channels like this:
ofColor myYellow;
myYellow.r = 255;
myYellow.b = 0;
myYellow.g = 255;
myYellow.a = 255;

// We can also make use of some predefined colors provided by openFrameworks:
ofColor myAqua = ofColor::aqua;
ofColor myPurple = ofColor::plum;
// Full list of colors available at: http://openframeworks.cc/documentation/types/ofColor.html
```
-->

```cpp
ofColor myOrange(255, 132, 0); // 不透明なオレンジ色の定義 - RGBによる指定
ofColor myBlue(0, 0, 255, 50); // 透明な青色の定義 - RGBAによる指定

// 赤、緑、青とアルファチャンネルにはこのようにアクセスできます
ofColor myGreen(0, 0, 255, 255);
cout << "Red channel:" << myGreen.r << endl;
cout << "Green channel:" << myGreen.g << endl;
cout << "Blue channel:" << myGreen.b << endl;
cout << "Alpha channel:" << myGreen.a << endl;

// 赤、緑、青とアルファチャンネルの設定もこのようにできます
ofColor myYellow;
myYellow.r = 255;
myYellow.b = 0;
myYellow.g = 255;
myYellow.a = 255;

// openFrameworksによって提供される既定の色も利用できます
ofColor myAqua = ofColor::aqua;
ofColor myPurple = ofColor::plum;
// 利用できる色の完全なリストはこちら: http://openframeworks.cc/documentation/types/ofColor.html
```

<!--
If we wanted to make our brush fierier, we would draw using random colors that are in-between orange and red. `ofColor` gives us in-betweenness using something called "[linear interpolation](https://en.wikipedia.org/wiki/Linear_interpolation)" with a function called [`getLerped(...)`](http://openframeworks.cc/documentation/types/ofColor.html#show_getLerped). `getLerped(...)` is a class method of `ofColor`, which means that if we have an `ofColor` variable, we can interpolate like this: `myFirstColor.getLerped(mySecondColor, 0.3)`. (For an explanation of classes and methods, see the _OOPS!_ chapter.) We pass in two arguments, an `ofColor` and a `float` value between `0.0` and `1.0`. The function returns a new `ofColor` that is between the two specified colors, and the `float` determines how close the new color is to our original color (here, `myFirstColor`). We can use this in `draw()` like this:
-->

ブラシをもっと燃えるような色にしたい場合、描画にオレンジと赤の間のランダムな色を使って描画すると良いでしょう。`ofColor`は[`getLerped(...)`](http://openframeworks.cc/documentation/types/ofColor.html#show_getLerped)という関数によって[線形補間（Linear interpolation）](https://en.wikipedia.org/wiki/Linear_interpolation)を利用し中間表現が可能です。`getLerped(...)`は`ofColor`のクラスメソッドで、こ
れは`ofColor`型の変数がある場合、`myFirstColor.getLerped(mySecondColor, 0.3)`のような補間が可能になります。（クラスメソッドの説明は _OOPS!_ の章をご覧ください。）我々は`ofColor`と`0.0`から`1.0`の間の`float`値という 2 つの引数を渡します。この関数は新しい`ofColor`を返し、これは指定された 2 つの色の中間で、`float`値は新しい色がどれだけ元の色（ここでは`myFirstColor`）に近いかを定義しています。これは`draw()`ではこのように利用できます。

<!--
```cpp
ofColor myOrange(255, 132, 0, alpha);
ofColor myRed(255, 6, 0, alpha);
ofColor inBetween = myOrange.getLerped(myRed, ofRandom(1.0));
ofSetColor(inBetween);
```
-->

```cpp
ofColor myOrange(255, 132, 0, alpha);
ofColor myRed(255, 6, 0, alpha);
ofColor inBetween = myOrange.getLerped(myRed, ofRandom(1.0));
ofSetColor(inBetween);
```

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_c_Glowing_Circle_Brush)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_c_Glowing_Circle_Brush.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_c_Glowing_Circle_Brush)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_c_Glowing_Circle_Brush.sketch)\]

<!--
#### Star Line Brush: Working with a Linear Map
-->

#### 星状の直線ブラシ：線形マッピングに触れる

<!--
What about lines? We are going to create a brush that draws lines that radiate out from the mouse to create something similar to an asterisk or a twinkling star (figure 7). Comment out the circle brush and add:
-->

さて、直線はどうでしょうか？マウスから放射状に線を引き、アスタリスクやきらめく星のようなものを作成してみましょう（図 7）。円のブラシをコメントアウトして、以下を追加します。

<!--
```cpp
int numLines = 30;
int minRadius = 25;
int maxRadius = 125;
for (int i=0; i<numLines; i++) {
    float angle = ofRandom(ofDegToRad(360.0));
    float distance = ofRandom(minRadius, maxRadius);
    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    float alpha = ofMap(distance, minRadius, maxRadius, 50, 0);  // Make shorter lines more opaque
    ofSetColor(255, alpha);
    ofDrawLine(ofGetMouseX(), ofGetMouseY(), ofGetMouseX()+xOffset, ofGetMouseY()+yOffset);
}
```
-->

```cpp
int numLines = 30;
int minRadius = 25;
int maxRadius = 125;
for (int i=0; i<numLines; i++) {
    float angle = ofRandom(ofDegToRad(360.0));
    float distance = ofRandom(minRadius, maxRadius);
    float xOffset = cos(angle) * distance;
    float yOffset = sin(angle) * distance;
    float alpha = ofMap(distance, minRadius, maxRadius, 50, 0);  // 短い直線ほど不透明にする
    ofSetColor(255, alpha);
    ofDrawLine(ofGetMouseX(), ofGetMouseY(), ofGetMouseX()+xOffset, ofGetMouseY()+yOffset);
}
```

<!--
What have we done with the alpha? We used [`ofMap(...)`](http://openframeworks.cc/documentation/math/ofMath.html#show_ofMap) to do a linear interpolation, similar to `getLerped(...)`. `ofMap(...)` transforms one range of values into a different range of values - like taking the "loudness" of a sound recorded on a microphone and using it to determine the color of a shape drawn on the screen. To get a "twinkle" effect, we want our shortest lines to be the most opaque and our longer lines to be the most transparent. `ofMap(...)` takes a value from one range and maps it into another range like this: `ofMap(value, inputMin, inputMax, outputMin, outputMax)`. We tell it that distance is a `value` in-between `minRadius` and `maxRadius` and that we want it mapped so that a distance value of 125 (`maxRadius`) returns an alpha value of 50 and a distance value of 25 (`minRadius`) returns an alpha value of 0.
-->

アルファ値について何をしたでしょう？[`ofMap(...)`](http://openframeworks.cc/documentation/math/ofMath.html#show_ofMap)を用いて、`getLerped(...)`に似た線形補間を行いました。`ofMap(...)`はある値の範囲を別の値の範囲に変換します。ちょうど、マイクで録音された音の「ラウドネス」を取って画面に描画される図形の色を決定するのに使うようなものです。「輝き」のエフェクトのために、短い直線は不透明に、直線が長くなるほど透明にしましょう。`ofMap(...)`は、`ofMap(value, inputMin, inputMax, outputMin, outputMax)`という風に、ある値の範囲を別の値の範囲にマッピングします。`value`は`minRadius`と`maxRadius`の間にあり、距離（distance）が 125（`maxRadius`）の場合にアルファ値として 50、距離が 25（`minRadius`）の時にアルファ値が 0 を返すように宣言しています。

<!--
We can also vary the line width using: `ofSetLineWidth(ofRandom(1.0, 5.0))`, but remember that if we change the line width in this brush, we will need go back and set our line width back to `1.0` in our other brushes.
-->

線幅も、`ofSetLineWidth(ofRandom(1.0, 5.0))`を用いて変化させています。しかしこのブラシの線幅を変化させた場合、別のブラシでは線幅を`1.0`に戻さなければならないであろうことを忘れないでください。

<!--
![Figure 7: Results from using the line brush](images/Figure7_LineStarBrush.png)
-->

![図7: 線のブラシを使った結果](images/Figure7_LineStarBrush.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_d_Star_Line_Brush)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_d_Star_Line_Brush.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_d_Star_Line_Brush)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_d_Star_Line_Brush.sketch)\]

<!--
#### Fleeing Triangle Brush: Vectors and Rotations
-->

#### 飛び散る三角形のブラシ：ベクトルと回転

<!--
Time for the last brush in section 1: the triangle. We'll draw a bunch of triangles that are directed outward from the mouse position (figure 8, left). `ofDrawTriangle(...)` requires us to specify the three corners of the triangle, which means that we will need to calculate the rotation of the corners to make the triangle point away from the mouse. A new class will make that math easier: [`ofVec2f`](http://openframeworks.cc/documentation/math/ofVec2f.html)\.
-->

セクション 1 の最後のブラシ、三角形です。マウスの位置から外側に向かう多数の三角形を描きましょう（図 8、左）。`ofDrawTriangle(...)`は三角形の 3 つの角を指定しないといけないですが、これはつまり角の回転を計算してマウスから外側を向くようにする必要があるということです。新しい[`ofVec2f`](http://openframeworks.cc/documentation/math/ofVec2f.html)クラスで計算が簡単にできます。

<!--
![Figure 8: Isosceles triangles in a brush, left, and isolated in a diagram, right](images/Figure8_IsoscelesTriangleDiagrams.png)
-->

![図 8: 二等辺三角形のブラシ（左）、 一つを図解したもの（右）](images/Figure8_IsoscelesTriangleDiagrams.png)

<!--
We've been defining points by keeping two separate variables: x and y. `ofVec2f` is a 2D vector, and for our purposes, we can just think of it as a point in 2D space. `ofVec2f` allows us to hold both x and y in a single variable (and perform handy math operations):
-->

これまで、x と y の変数を独立して保持することで点を定義してきました。`ofVec2f`は 2 次元ベクトルで、我々の目的にとってはちょうど 2 次元空間における点であると考えることができます。`ofVec2f`は一つの変数で x と y を保持（加えて便利な数学的計算も）することができます。

<!--
```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());  // Defining a new ofVec2f

// Access the x and y coordinates like this:
cout << "Mouse X: " << mousePos.x << endl;
cout << "Mouse Y: " << mousePos.y << endl;

// Or we can modify the coordinates like this:
float xOffset = 10.0;
float yOffset = 30.0;
mousePos.x += xOffset;
mousePos.y += yOffset;

// But we can do what we just did above by adding or subtracting two vectors directly
ofVec2f offset(10.0, 30.0);
mousePos += offset;
```
-->

```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());  // ofVec2fを新しく定義

// xとy座標にはこのようにアクセスします
cout << "Mouse X: " << mousePos.x << endl;
cout << "Mouse Y: " << mousePos.y << endl;

// 座標はこのように変更できます
float xOffset = 10.0;
float yOffset = 30.0;
mousePos.x += xOffset;
mousePos.y += yOffset;

// 上記で行ったことは2つのベクトルを直接加減することで直接行えます。
ofVec2f offset(10.0, 30.0);
mousePos += offset;
```

<!--
Let's start using it to build the triangle brush. The first step is to draw a triangle (figure 8, right) at the mouse cursor. It will become important later, but we are going to draw our triangle starting from the mouse cursor and pointing to the right. Comment out the line brush, and add:
-->

手始めに三角形のブラシを作成してみましょう。最初のステップはマウスカーソルの位置に三角形を描画してみます（図 8、右）。後ほど重要になりますが、マウスの位置から開始して右向きの三角形を描くことにしましょう。直線の描画をコメントアウトして、以下を追加します。

<!--
```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());

// Define a triangle at the origin (0,0) that points to the right
ofVec2f p1(0, 25.0);
ofVec2f p2(100, 0);
ofVec2f p3(0, -25.0);

// Shift the triangle to the mouse position
p1 += mousePos;
p2 += mousePos;
p3 += mousePos;

ofSetColor(255, 50);
ofDrawTriangle(p1, p2, p3);
```
-->

```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());

// 原点が(0,0)で右向きの三角形を定義します
ofVec2f p1(0, 25.0);
ofVec2f p2(100, 0);
ofVec2f p3(0, -25.0);

// 三角形をマウス位置まで移動します
p1 += mousePos;
p2 += mousePos;
p3 += mousePos;

ofSetColor(255, 50);
ofDrawTriangle(p1, p2, p3);
```

<!--
Run it and see what happens. We can add rotation with the `ofVec2f` class method [`rotate(...)`](http://openframeworks.cc/documentation/math/ofVec2f.html#show_rotate) like this: `myPoint.rotate(45.0)` where `myPoint` is rotated around the origin, `(0, 0)`, by `45.0` degrees. Back to our code, add this right before shifting the triangle to the mouse position:
-->

実行してどうなるかみてみましょう。`ofVec2f`クラスの[`rotate(...)`](http://openframeworks.cc/documentation/math/ofVec2f.html#show_rotate)を使って`myPoint.rotate(45.0)`という風に回転を加えることができます。ここでは`myPoint`が原点`(0, 0)`を中心に`45.0`度回転します。コードに戻って、マウス位置に三角形を移動させる直前にこれを追加しましょう。

<!--
```cpp
// Rotate the triangle points around the origin
float rotation = ofRandom(360); // The rotate function uses degrees!
p1.rotate(rotation);
p2.rotate(rotation);
p3.rotate(rotation);
```
-->

```cpp
// 原点を中心に三角形を回転させる
float rotation = ofRandom(360); // rotate関数は角度（degree）を使います！
p1.rotate(rotation);
p2.rotate(rotation);
p3.rotate(rotation);
```

<!--
![Figure 9: Results from using the rotating triangle brush](images/Figure9_RotatingTriangleBrush.png)
-->

![図 9: 三角形を回転させた結果のブラシ](images/Figure9_RotatingTriangleBrush.png)

<!--
Our brush looks something like figure 8 (left). If we were to move that rotation code to _after_ we shifted the triangle position, the code wouldn't work very nicely because `rotate(...)` assumes we want to rotate our point around the origin. (Check out the documentation for an alternate way to use `rotate(...)` that rotates around an arbitrary point.) Last step, let's integrate our prior approach of drawing multiple shapes that are offset from the mouse:
-->

ブラシは図 8（左）のように見えます。`rotate(...)`は原点を中心に点を回転させるとみなすので、もし回転のコードを三角形の移動の _後ろ_ に移動させた場合にはうまく動作しないでしょう（任意の点を中心に回転させる`rotate(...)`の使い方はドキュメントを参照してください）。最後のステップとして、これまでのアプローチをまとめて、複数の図形をマウス位置からずらした位置に描画してみましょう。

<!--
```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());

int numTriangles = 10;
int minOffset = 5;
int maxOffset = 70;
int alpha = 150;
for (int t=0; t<numTriangles; t++) {
    float offsetDistance = ofRandom(minOffset, maxOffset);

    // Define a triangle at the origin (0,0) that points to the right (code omitted)
    // The triangle size is a bit smaller than the last brush - see the source code

    // Rotate the triangle (code omitted)

    ofVec2f triangleOffset(offsetDistance, 0.0);
    triangleOffset.rotate(rotation);

    p1 += mousePos + triangleOffset;
    p2 += mousePos + triangleOffset;
    p3 += mousePos + triangleOffset;

    ofSetColor(255, alpha);
    ofDrawTriangle(p1, p2, p3);
}
```
-->

```cpp
ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());

int numTriangles = 10;
int minOffset = 5;
int maxOffset = 70;
int alpha = 150;
for (int t=0; t<numTriangles; t++) {
    float offsetDistance = ofRandom(minOffset, maxOffset);

    // 原点(0, 0)から右向きの三角形を定義（コードは省略）
    // 最後のブラシよりも三角形のサイズは少し小さいです - ソースコードを参照

    // 三角形を回転（コード省略）

    ofVec2f triangleOffset(offsetDistance, 0.0);
    triangleOffset.rotate(rotation);

    p1 += mousePos + triangleOffset;
    p2 += mousePos + triangleOffset;
    p3 += mousePos + triangleOffset;

    ofSetColor(255, alpha);
    ofDrawTriangle(p1, p2, p3);
}
```

<!--
We are now using `ofVec2f` for our offset. We started with a vector that points rightward, the same direction our triangle starts out pointing. When we apply the rotation to them both, they stay in sync (i.e. both pointing away from the mouse). We can push them out of sync with: `triangleOffset.rotate(rotation+90)`, and we get a swirling blob of triangles. After that, we can add some color using `ofRandom(...)` and `getLerped(...)` again (figure 9) or play with fill and line width.
-->

`ofVec2f`をオフセットに利用しています。はじめは三角形が向いているのと同じ向きの、右向きのベクトルです。これらに回転を適用する際、これらは同期します（つまりマウス位置から外側を向く）。`triangleOffset.rotate(rotation+90)`で同期させないようにして、渦巻く三角形を作る事もできます。このあとで、`ofRandom(...)`や`getLerped(...)`を使って色を加えたり（図 9）塗りつぶしや線幅で遊んでみても良いでしょう。

<!--
![Figure 10: Results from using the final triangle brush](images/Figure10_TriangleSwirlBrush.png)
-->

![図 10: 完成した三角形ブラシの結果](images/Figure10_TriangleSwirlBrush.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush.sketch)\]

<!--
**Extensions**
-->

**発展**

<!--
1. Define some public variables to control brush parameters like `transparency`, `brushWidth`, `offsetDistance`, `numberOfShapes`, etc.
2. Use the [`keyPressed(int key)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_keyPressed) function (in `.cpp`) to control those parameters at run time (e.g. increasing/decreasing `brushWidth` with the `+` and `-` keys). If you are using ofSketch, see the next section for how to use that function.
3. Track the mouse position and use the distance it moves between frames to control those parameters (e.g. fast moving mouse draws a thicker brush).
-->

1. `透明度（transparency）`、`ブラシ幅（brushWidth）`、`オフセット距離（offsetDistance）`、`図形の数（numberOfShapes）`等のパブリックな変数を定義してブラシのパラメタを制御してみましょう。
2. [`keyPressed(int key)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_keyPressed)関数を（`.cpp`の中で）使って、実行時にそれらのパラメータを制御してみましょう（例 `+`と`-`キーで`ブラシ幅（brushWidth）`を増加/減少させる）。ofSketch を使っているのであれば、次のセクションでこの関数をどう使うかをご覧ください。
3. マウス位置をトラッキングし、フレーム間で移動した距離でパラメータを制御してみましょう（例 マウスを速く動かすとブラシが濃くなる）。

<!--
#### Raster Graphics: Taking a Snapshot
-->

#### ラスターグラフィックス：スナップショットの撮影

<!--
Before we move on, let's save a snapshot of our canvas. We'll want to use the [`keyPressed(int key)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_keyPressed) function. This function is built into your application by default. Any time a key is pressed, the code you put into this function is called. The `key` variable is an integer that represents the key that was pressed.
-->

続ける前に、キャンバスのスナップショットを保存しましょう。[`keyPressed(int key)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_keyPressed)関数を利用します。この関数はアプリケーションにデフォルトで組み込まれています。キーが押されるといつでも、この関数の中に書かれたコードが呼ばれます。`key`変数は整数で、押されたキーを示します。

<!--
If you are using project generator, you'll find `keyPressed(...)` in your `.cpp` file. If you are using ofSketch, you might not see the function, but it is easy to add. See the [ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush.sketch) for the last section.
-->

project generator を利用しているならば、`keyPressed(...)`は`.cpp`ファイルの中にあります。ofSketch を利用している場合、この関数は見当たらないかもしれませんが、簡単に追加できます。[ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/1_ii_e_Triangle_Brush.sketch)の最後のセクションをみてください。

<!--
In the `keyPressed(...)` function, add the following:
-->

`keyPressed(...)`関数に、以下を追加しましょう。

<!--
```cpp
if (key == 's') {
    // It's strange that we can compare the int key to a character like `s`, right?  Well, the super short
    // explanation is that characters are represented by numbers in programming.  `s` and 115 are the same
    // thing.  If you want to know more, check out the wiki for ASCII.
    glReadBuffer(GL_FRONT);  // HACK: only needed on windows, when using ofSetAutoBackground(false)
    ofSaveScreen("savedScreenshot_"+ofGetTimestampString()+".png");
}
```
-->

```cpp
if (key == 's') {
    // `s`のような文字と整数型のキーを比較しているのは奇妙に見えるでしょうか？
    // よろしい、とても短い答えは、プログラミングでは文字は数値として表現されているからです。
    // `s`と115は同じものです。もっと知りたければ、ASCIIについてのwikiを参照してください。
    glReadBuffer(GL_FRONT);  // HACK: only needed on windows, when using ofSetAutoBackground(false)
    ofSaveScreen("savedScreenshot_"+ofGetTimestampString()+".png");
}
```

<!--
[`ofSaveScreen(...)`](http://openframeworks.cc/documentation/utils/ofUtils.html#show_ofSaveScreen) grabs the current screen and saves it to a file inside of our project's `./bin/data/` folder with a filename we specify. The timestamp is used to create a unique filename, allowing us to save multiple screenshots without worrying about them overriding each other. So press the `s` key and check out your screenshot!
-->

[`ofSaveScreen(...)`](http://openframeworks.cc/documentation/utils/ofUtils.html#show_ofSaveScreen)は現在のスクリーンをキャプチャしてそれをプロジェクトの中の`./bin/data/`フォルダの中に指定したファイル名で保存します。タイムスタンプをユニークなファイル名を作成するために使っていますが、これで複数のスクリーンショットが互いに上書きされる心配なく保存できます。さて`s`キーを押してスクリーンショットを確認してみましょう！

<!--
## Brushes from Freeform Shapes
-->

## 自由形状を用いたブラシ

<!--
In the last section, we drew directly onto the screen. We were storing graphics (brush strokes) as pixels, and therefore working with [raster graphics](https://en.wikipedia.org/wiki/Raster_graphics). For this reason, it is hard to isolate, move or erase a single brush stroke. It also means we can't re-render our graphics at a different resolution. In contrast, [vector graphics](https://en.wikipedia.org/wiki/Vector_graphics) store graphics as a list of geometric objects instead of pixel values. Those objects can be modified (erased, moved, rescaled, etc.) after we "place" them on our screen.
-->

先ほどのセクションでは、画面に直接描画を行いました。グラフィック（ブラシの軌跡）はピクセルで保存していますので、つまり[ラスターグラフィックス](https://en.wikipedia.org/wiki/Raster_graphics)を扱っています。このため、ブラシの軌跡を個別に移動させたり消去したりすることは困難です。

<!--
In this section, we are going to make a kind of vector graphics by using custom ("freeform") shapes in openFrameworks. We will use structures (`ofPolyline` and `vector<ofPolyline>`) that allow us to store and draw the path that the mouse takes on the screen. Then we will play with those paths to create brushes that do more than just trace out the cursor's movement.
-->

このセクションでは、openFrameworks で独自（自由な）形状を利用してベクタグラフィックスを作ってみましょう。構造体（`ofPolyline` と `vector<ofPolyline>`）を使ってスクリーン上のマウスの軌跡を保存して描画します。それからこのパスを利用して、単にカーソルの動きを追随するだけ以上のブラシを作成してみます。

<!--
### Basic Polylines
-->

### 基本的なポリライン

<!--
Create a new project called "Polylines," and say hello to [`ofPolyline`](http://openframeworks.cc/documentation/graphics/ofPolyline.html). `ofPolyline` is a data structure that allows us to store a series of sequential points and then connect them to draw a line. Let's dive into some code. In your header file (inside "class ofApp" in "ofApp.h" to be precise), define three `ofPolylines`:
-->

"Polylines"という名前の新規プロジェクトを作成して、[`ofPolyline`](http://openframeworks.cc/documentation/graphics/ofPolyline.html)を見てみましょう。`ofPolyline`は順序だった点の連なりを保存して連結し、線を描画することのできるデータ構造です。コードを見てみましょう。ヘッダファイル（正確には"ofApp.h"の"class ofApp"の中）に 3 つの`ofPolylines`を宣言します。

<!--
```cpp
ofPolyline straightSegmentPolyline;
ofPolyline curvedSegmentPolyline;
ofPolyline closedShapePolyline;
```
-->

```cpp
ofPolyline straightSegmentPolyline;
ofPolyline curvedSegmentPolyline;
ofPolyline closedShapePolyline;
```

<!--
We can fill those `ofPolylines` with points in `setup()`:
-->

この`ofPolylines`には`setup()`で点を追加できます。

<!--
```cpp
straightSegmentPolyline.addVertex(100, 100);  // Add a new point: (100, 100)
straightSegmentPolyline.addVertex(150, 150);  // Add a new point: (150, 150)
straightSegmentPolyline.addVertex(200, 100);  // etc...
straightSegmentPolyline.addVertex(250, 150);
straightSegmentPolyline.addVertex(300, 100);

curvedSegmentPolyline.curveTo(350, 100);  // These curves are Catmull-Rom splines
curvedSegmentPolyline.curveTo(350, 100);  // Necessary Duplicate for Control Point
curvedSegmentPolyline.curveTo(400, 150);
curvedSegmentPolyline.curveTo(450, 100);
curvedSegmentPolyline.curveTo(500, 150);
curvedSegmentPolyline.curveTo(550, 100);
curvedSegmentPolyline.curveTo(550, 100);  // Necessary Duplicate for Control Point

closedShapePolyline.addVertex(600, 125);
closedShapePolyline.addVertex(700, 100);
closedShapePolyline.addVertex(800, 125);
closedShapePolyline.addVertex(700, 150);
closedShapePolyline.close();  // Connect first and last vertices
```
-->

```cpp
straightSegmentPolyline.addVertex(100, 100);  // 新規の点を追加: (100, 100)
straightSegmentPolyline.addVertex(150, 150);  // 新規の点を追加: (150, 150)
straightSegmentPolyline.addVertex(200, 100);  // 等々...
straightSegmentPolyline.addVertex(250, 150);
straightSegmentPolyline.addVertex(300, 100);

curvedSegmentPolyline.curveTo(350, 100);  // これらの曲線はキャットムル-ロム（Catmull-Rom）スプライン
curvedSegmentPolyline.curveTo(350, 100);  // 制御点として必要な重複です
curvedSegmentPolyline.curveTo(400, 150);
curvedSegmentPolyline.curveTo(450, 100);
curvedSegmentPolyline.curveTo(500, 150);
curvedSegmentPolyline.curveTo(550, 100);
curvedSegmentPolyline.curveTo(550, 100);  // 制御点として必要な重複です

closedShapePolyline.addVertex(600, 125);
closedShapePolyline.addVertex(700, 100);
closedShapePolyline.addVertex(800, 125);
closedShapePolyline.addVertex(700, 150);
closedShapePolyline.close();  // 最初と最後の点を結合
```

<!--
We can now draw our polylines in the `draw()` function:
-->

これで`draw()`関数の中でポリラインを描画できます。

<!--
```cpp
ofBackground(0);
ofSetLineWidth(2.0);  // Line widths apply to polylines
ofSetColor(255,100,0);
straightSegmentPolyline.draw();  // This is how we draw polylines
curvedSegmentPolyline.draw();  // Nice and easy, right?
closedShapePolyline.draw();
```
-->

```cpp
ofBackground(0);
ofSetLineWidth(2.0);  // ポリラインに適用する線幅
ofSetColor(255,100,0);
straightSegmentPolyline.draw();  // これはポリラインの描画方法です
curvedSegmentPolyline.draw();  // いい感じだし簡単ですよね？
closedShapePolyline.draw();
```

<!--
We created three different types of polylines (figure 11). `straightSegmentPolyline` is composed of a series points connected with straight lines. `curvedSegmentPolyline` uses the same points but connects them with curved lines. The curves that are created are [Catmull–Rom splines](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline), which use four points to define a curve: two define the start and end, while two control points determine the curvature. These control points are the reason why we need to add the first and last vertex twice. Lastly, `closedShapePolyline` uses straight line segments that are closed, connecting the first and last vertices.
-->

3 つの異なるタイプのポリラインを作成しました（図 11）。`straightSegmentPolyline`は直線で繋がれた一連の点で構成されています。`curvedSegmentPolyline`は同じ点を利用しますが、それらは曲線で接続されています。作成された曲線は[キャットムル-ロム（Catmull-Rom）スプライン](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline)で、これは曲線を定義するのに点を 4 つ使い、始点と終点で 2 つ、2 つの制御点が曲率を決めます。この制御点が最初と最後の点を 2 回追加した理由です。最後に、`closedShapePolyline`は最初と最後の点を繋いだ閉じた直線を利用します。

<!--
![Figure 11: Examples of polylines - straight, curved and closed straight](images/Figure11_PolylineExamples.png)
-->

![図 11: ポリラインの例 - 直線、曲線および閉じた直線](images/Figure11_PolylineExamples.png)

<!--
The advantage of drawing in this way (versus raster graphics) is that the polylines are modifiable. We could easily move, add, delete, scale our vertices on the the fly.
-->

このように描画する（ラスタグラフィックスに対する）利点は、ポリラインは調整できるということです。実行中に点を容易に移動、追加、削除、拡縮することができます。

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_i_Basic_Polylines)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_i_Basic_Polylines.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_i_Basic_Polylines)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_i_Basic_Polylines.sketch)\]

<!--
**Extensions**
-->

**発展**

<!--
1. Check out [`arc(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_arc), [`arcNegative(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_arcNegative) and [`bezierTo(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_bezierTo) for other ways to draw shapes with `ofPolyline`.
-->

1. [`arc(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_arc)、 [`arcNegative(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_arcNegative) と [`bezierTo(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_bezierTo)をチェックして`ofPolyline`を使って形状を描画するその他の方法を見てみましょう。

<!--
### Building a Brush from Polylines
-->

### ポリラインからブラシを作成する

<!--
#### Polyline Pen: Tracking the Mouse
-->

#### ポリラインのペン：マウスのトラッキング

<!--
Let's use polylines to draw brush strokes. Create a new project, "PolylineBrush." When the left mouse button is held down, we will create an `ofPolyline` and continually extend it to the current mouse position. We will use a `bool` to tell us if the left mouse button is being held down. If it is being held down, we'll add the mouse position to the polyline, but instead of adding _every_ mouse position, we'll add the mouse positions where the mouse has moved a distance away from the last point in our polyline.
-->

ブラシの軌跡を描くのにポリラインを利用してみましょう。新規プロジェクトを作成して"PolylineBrush”という名前にします。マウスの左ボタンが押下されている間、`ofPolyline`を作成して現在のマウス位置まで継続的に延長していきます。`bool`を使って左マウスボタンが押下されているかどうかを判別します。押下されている間は、ポリライン（Polyline）にマウス位置を追加しますが、マウス位置を _全て_ 追加するのではなく、最後の場所からある程度移動した場合にポリラインにマウス位置を追加します。

<!--
Let's move on to the code. Create four variables in the header:
-->

コードに移りましょう。ヘッダで 4 つの変数を作成します。

<!--
```cpp
ofPolyline currentPolyline;
bool leftMouseButtonPressed;
ofVec2f lastPoint;
float minDistance;
```
-->

```cpp
ofPolyline currentPolyline;
bool leftMouseButtonPressed;
ofVec2f lastPoint;
float minDistance;
```

<!--
Initialize `minDistance` and `leftMouseButtonPressed` in `setup()`:
-->

`minDistance` と `leftMouseButtonPressed` を `setup()` で初期化します。

<!--
```cpp
minDistance = 10;
leftMouseButtonPressed = false;
```
-->

```cpp
minDistance = 10;
leftMouseButtonPressed = false;
```

<!--
Now we are going to take advantage of two new functions - [`mousePressed(int x, int y, int button)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_mousePressed) and [`mouseReleased(int x, int y, int button)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#show_mouseReleased). These are functions that are built into your application by default. They are event handling functions, so whenever a mouse button is pressed, whatever code you put into `mousePressed(...)` is called. It's important to note that `mousePressed(...)` is only called when the mouse button is initially pressed. No matter how long we hold the mouse button down, the function is still only called once. The same goes for `mouseReleased(...)`.
-->

ここで [`mousePressed(int x, int y, int button)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_mousePressed) そして [`mouseReleased(int x, int y, int button)`](http://openframeworks.cc/documentation/application/ofBaseApp.html#show_mouseReleased) という 2 つの新しい関数を利用してみましょう。これらはアプリケーションにデフォルトで組み込まれています。これらはイベントハンドリングの関数で、したがってマウスボタンが押下されればいつでも、`mousePressed(...)` に書かれたコードが呼ばれます。`mousePressed(...)`はマウスが最初に押された時だけ呼ばれることは注意しておくべきでしょう。マウスボタンをどれだけ長く押下し続けていても、この関数は一度しか呼ばれません。`mouseReleased(...)` も同様です。

<!--
The functions have a few variables `x`, `y` and `button` that allow you to know a bit more about the particular mouse event that just occurred. `x` and `y` are the screen coordinates of the cursor, and `button` is an `int` that represents the particular button on the mouse that was pressed/released. Remember the public constants like `OF_MOUSE_BUTTON_LEFT` and `OF_MOUSE_BUTTON_RIGHT`? To figure out what `button` is, we'll compare it against those constants.
-->

この関数は `x`、`y` そして `button` の変数があって、今まさに発生した固有のマウスイベントについてより詳しく知ることができます。`x` と `y` はカーソルのスクリーン上での座標、`button` は `int` 型で、押された/離されたマウスボタンを表しています。`OF_MOUSE_BUTTON_LEFT` や `OF_MOUSE_BUTTON_RIGHT` といったパブリック定数を覚えていますか？`button` がどれかを知るにはこれらの定数との比較を行います。

<!--
Let's turn back to the code. If you are using project generator, you'll find these mouse functions in your `.cpp` file. If you are using ofSketch, you might not see these functions, but they are easy to add. See the [ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch) for this section. Inside of `mousePressed(...)`, we want to start the polyline:
-->

コードに戻りましょう。project generator を利用している場合は、マウス関数は `.cpp` ファイルの中にあります。ofSketch を使っている場合はこれらの関数がありませんが、簡単に追加することができます。このセクションの[ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch)を見てみてください。`mousePressed(...)` の中で、ポリラインを開始しましょう。

<!--
```cpp
if (button == OF_MOUSE_BUTTON_LEFT) {
    leftMouseButtonPressed = true;
    currentPolyline.curveTo(x, y);  // Remember that x and y are the location of the mouse
    currentPolyline.curveTo(x, y);  // Necessary duplicate for first control point
    lastPoint.set(x, y);  // Set the x and y of a ofVec2f in a single line
}
-->

```cpp
if (button == OF_MOUSE_BUTTON_LEFT) {
    leftMouseButtonPressed = true;
    currentPolyline.curveTo(x, y);  // xとyはマウスの位置です
    currentPolyline.curveTo(x, y);  // 最初の制御点のために必要な重複です
    lastPoint.set(x, y);  // ofVec2fのxとyを単一の線に設定します
}

```

<!--
Inside of `mouseReleased(...)`, we want to end the polyline:
-->

`mouseReleased(...)`の中でポリラインを終了します。
Inside of `mouseReleased(...)`, we want to end the polyline:

<!--
```cpp
if (button == OF_MOUSE_BUTTON_LEFT) {
    leftMouseButtonPressed = false;
    currentPolyline.curveTo(x, y); // Necessary duplicate for last control point
    currentPolyline.clear();  // Erase the vertices, allows us to start a new brush stroke
}
```
-->

```cpp
if (button == OF_MOUSE_BUTTON_LEFT) {
    leftMouseButtonPressed = false;
    currentPolyline.curveTo(x, y); // 最後の制御点のために必要な重複です
    currentPolyline.clear();  // 頂点を消去して新しいブラシのストロークを開始できるようにします
}
```

<!--
Now let's move over to the `update()` function. For ofSketch users, this is another default function that you might not see in your sketch. It is a function that is called once per frame, and it is intended for doing non-drawing tasks. It's easy to add - see the [ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch) for this section.
-->

`update()` 関数に行ってみましょう。ofSketch ユーザーは、こちらも sketch では見つけられないデフォルト関数です。これはフレームごとに一回、描画以外のタスクのために呼ばれる関数です。簡単に追加することができますので、このセクションの[ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch)をご覧ください。

<!--
Let's add points to our polyline in `update()`:
-->

`update()` でポリラインに点を追加しましょう。

<!--
```cpp
if (leftMouseButtonPressed) {
    ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());
    if (lastPoint.distance(mousePos) >= minDistance) {
        // a.distance(b) calculates the Euclidean distance between point a and b.  It's
        // the length of the straight line distance between the points.
        currentPolyline.curveTo(mousePos);  // Here we are using an ofVec2f with curveTo(...)
        lastPoint = mousePos;
    }
}
```
-->

```cpp
if (leftMouseButtonPressed) {
    ofVec2f mousePos(ofGetMouseX(), ofGetMouseY());
    if (lastPoint.distance(mousePos) >= minDistance) {
        // a.distance(b) は点aとbの間のユークリッド距離を計算します。
        // これは点の間の直線距離です。
        currentPolyline.curveTo(mousePos);  // curveTo(...)にofVec2fを利用します
        lastPoint = mousePos;
    }
}
```

<!--
Note that this only adds points when the mouse has moved a certain threshold amount (`minDistance`) away from the last point we added to the polyline. This uses the [`distance(...)`](http://openframeworks.cc/documentation/math/ofVec2f.html#show_distance) method of `ofVec2f`.
-->

ポリラインに追加した最後の場所から特定のしきい値（`minDistance`）移動した場合にだけ点を追加していることに注目してください。これは `ofVec2f` の [`distance(...)`](http://openframeworks.cc/documentation/math/ofVec2f.html#show_distance) メソッドを利用しています。

<!--
All that is left is to add code to draw the polyline in `draw()`, and we've got a basic curved polyline drawing program. But we don't have the ability to save multiple polylines, so we have something similar to an [Etch A Sketch](https://en.wikipedia.org/wiki/Etch_A_Sketch). We can only draw a single, continuous line. In order to be able to draw multiple lines that don't have to be connected to each other, we will turn to something called a `vector`. This isn't the same kind of vector that we talked about earlier in the context of `of2Vecf`. If you haven't seen vectors before, check out the [stl::vector basics tutorial](http://openframeworks.cc/ofBook/chapters/stl_vector.html) on the site.
-->

残すは`draw()`の中でポリラインを描画するコードを追加することで、すでに基本的なポリライン描画のプログラムはありますが、複数のポリラインを保存することはできませんので、[Etch A Sketch](https://en.wikipedia.org/wiki/Etch_A_Sketch)に似たことをやりましょう。可能なことは、単一の連続する線を描画することだけです。違いに連結していない複数の線を描画できるようにするために、`vector`というものを使います。これは`of2Vecf`の文脈で先述したベクター（vector）と同じ種類のものではありません。もしこれまでにベクターを見ていなければ、このサイトの[stl::vector basics tutorial](http://openframeworks.cc/ofBook/chapters/stl_vector.html)を参照してください。
Define `vector <ofPolyline> polylines` in the header. We will use it to save our polyline brush strokes. When we finish a stroke, we want to add the polyline to our vector. So in the if statement inside of `mouseReleased(...)`, before `currentPolyline.clear()`, add `polylines.push_back(currentPolyline)`. Then we can draw the polylines like this:

<!--
```cpp
ofBackground(0);
ofSetColor(255);  // White color for saved polylines
for (int i=0; i<polylines.size(); i++) {
    ofPolyline polyline = polylines[i];
    polyline.draw();
}
ofSetColor(255,100,0);  // Orange color for active polyline
currentPolyline.draw();
```
-->

```cpp
ofBackground(0);
ofSetColor(255);  // 保存されたポリラインは白色です
for (int i=0; i<polylines.size(); i++) {
    ofPolyline polyline = polylines[i];
    polyline.draw();
}
ofSetColor(255,100,0);  // アクティブなポリラインはオレンジ色にします
currentPolyline.draw();
```

<!--
And we have a simple pen-like brush that tracks the mouse, and we can draw a dopey smiley face (figure 12).
-->

マウスを追随する単純なペンのようなブラシで、まぬけなスマイル顔（図 12）を描画してみましょう。

<!--
![Figure 12: Drawing a smilie with the polyline brush](images/Figure12_PolylineSmilie.png)
-->

![図 12: ポリラインブラシでのスマイリーの描画](images/Figure12_PolylineSmilie.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_a_Polyline_Pen.sketch)\]

<!--
**Extensions**
-->

**発展**

<!--
1. Add color!
2. Explore [`ofBeginSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofBeginSaveScreenAsPDF) and [`ofEndSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofEndSaveScreenAsPDF) to save your work into a vector file format.
3. Try using the `keyPressed(...)` function in your source file to add an undo feature that deletes the most recent brush stroke.
4. Try restructuring the code to allow for a redo feature as well.
-->

1. 色を追加しましょう！
2. [`ofBeginSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofBeginSaveScreenAsPDF) と [`ofEndSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofEndSaveScreenAsPDF) を見て、作品をベクターファイルの形式で保存してみましょう。
3. `keyPressed(...)` 関数を使って m 最後のブラシの軌跡を削除するようなアンドゥ機能を追加してみましょう。
4. 同様にリドゥの機能が可能なようにソースコードを再構成してみましょう。

<!--
#### Polyline Brushes: Points, Normals and Tangents
-->

#### ポリラインのブラシ：点、法線、接線

<!--
Since we have the basic drawing in place, now we play with how we are rendering our polylines. We will draw points, normals and tangents. We'll talk about what normals and tangents are in a little bit. First, let's draw points (circles) at the vertices in our polylines. Inside the `for` loop in `draw()` (after `polyline.draw()`), add this:
-->

これで基本的な描画はできましたので、ポリラインの描画の方法を試してみましょう。点、法線そして接線を描画してみます。もうすぐ法線と接線とはなんなのかは説明します。まずは、ポリラインの頂点に点（円）を描画してみましょう。`draw()`の中の`for`ループ（`polyline.draw()`の後ろ）の中に、以下を追加します。

<!--
```cpp
vector<ofVec3f> vertices = polyline.getVertices();
for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
    ofVec3f vertex = vertices[vertexIndex];  // ofVec3f is like ofVec2f, but with a third dimension, z
    ofDrawCircle(vertex, 5);
}
```
-->

```cpp
vector<ofVec3f> vertices = polyline.getVertices();
for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
    ofVec3f vertex = vertices[vertexIndex];  // ofVec3fはofVec2fに似ていますが、3次元です
    ofDrawCircle(vertex, 5);
}
```

<!--
[`getVertices()`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getVertices) returns a `vector` of `ofVec3f` objects that represent the vertices of our polyline. This is basically what an `ofPolyline` is - an ordered set of `ofVec3f` objects (with some extra math). We can loop through the indices of the vector to pull out the individual vertex locations, and use them to draw circles.
-->

[`getVertices()`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getVertices) はポリラインの頂点を表す`ofVec3f`オフジェクトの`vector`を返します。これはそもそもが`ofPolyline`とは何であるか、`ofVec3f`オフジェクトの順序付き（それ追加のいくらかの数学）、ということです。ベクターの要素を走査して、個々の頂点の位置を取得し、円の描画に利用します。

<!--
What happens when we run it? Our white lines look thicker. That's because our polyline is jam-packed with vertices! Every time we call the `curveTo(...)` method, we create 20 extra vertices (by default). These help make a smooth-looking curve. We can adjust how many vertices are added with an optional parameter, `curveResolution`, in `curveTo(...)`. We don't need that many vertices, but instead of lowering the `curveResolution`, we can make use of [`simplify(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_simplify)\.
-->

これを実行すると何が起きるでしょうか？白線が太くなったように見えます。これはポリラインが頂点だらけだからです！`curveTo(...)`メソッドを呼ぶたびに、（デフォルトでは）20 個の頂点が追加されています。これで曲線が滑らかに見えているのです。`curveTo(...)`の`curveResolution`という追加のパラメータでいくつの頂点が追加されるかは調整ができます。これほど多くの頂点は必要でありませんが、`curveResolution`を減らす代わりに、[`simplify(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_simplify)を使うことができます。

<!--
`simplify(...)` is a method that will remove "duplicate" points from our polyline. We pass a single argument into it: `tolerance`, a value between 0.0 and 1.0. The `tolerance` describes how dis-similar points must be in order to be considered 'unique' enough to not be deleted. The higher the `tolerance`, the more points will be removed. So right before we save our polyline by putting it into our `polylines` vector, we can simplify it. Inside of the if statement within `mouseReleased(...)` (before `polylines.push_back(currentPolyline)`), add: `currentPolyline.simplify(0.75)`. Now we should see something like figure 13 (left).
-->

`simplify(...)`は、「重複した」点をポリラインから除いてくれるメソッドです。これには一つの引数を渡しますが、これは`torelance（許容度）`という 0.0 から 1.0 の間の値です。この`torelance`は、個々の点がどのよう削除されないように「ユニーク（独立）である」と見なされるか、を指定します。`torelance`が高ければ、より多くの点が削除されます。したがってポリラインを`polylines`ベクターに追加して保存する前に、これを単純化しましょう。（`polylines.push_back(currentPolyline)`の前の）`mouseReleased(...)`の中の if ステートメントの中に`currentPolyline.simplify(0.75)`を追加します。これで図 13（左）のようになるでしょう。

<!--
![Figure 13: Drawing circles at the vertices of a polyline, without and with resampling points evenly](images/Figure13_PolylinePoints.png)
-->

![図 13：ポリラインの頂点に円を描画、点の再サンプリングの無しと有り](images/Figure13_PolylinePoints.png)

<!--
We can also sample points along the polyline using [`getPointAtPercent(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getPointAtPercent), which takes a `float` between `0.0` and `1.0` and returns a `ofVec3f`. Inside the `draw()` function, comment out the code that draws a circle at each vertex. Below that, add:
-->

[`getPointAtPercent(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getPointAtPercent)を使って点を再サンプルすることも可能で、これは`0.0`から`1.0`の間の`float`を受け取って`ofVec3f`を返します。`draw()`関数の中で、各々の頂点で円を描画するコードをコメントアウトします。その下に、下記を追加します。

<!--
```cpp
    for (int p=0; p<100; p+=10) {
        ofVec3f point = polyline.getPointAtPercent(p/100.0);  // Returns a point at a percentage along the polyline
        ofDrawCircle(point, 5);
    }
```
-->

```cpp
    for (int p=0; p<100; p+=10) {
        ofVec3f point = polyline.getPointAtPercent(p/100.0);  // Returns a point at a percentage along the polyline
        ofDrawCircle(point, 5);
    }
```

<!--
Now we have evenly spaced points (figure 13, right). (Note that there is no circle drawn at the end of the line.) Let's try creating a brush stroke where the thickness of the line changes. To do this we need to use a [normal vector](https://en.wikipedia.org/w/index.php?title=Normal_vector). Figure 14 shows normals drawn over some polylines - they point in the opposite (perpendicular) direction to the polyline. Imagine drawing a normal at every point along a polyline, like figure 15. That is one way to add "thickness" to our brush. We can comment out our circle drawing code in `draw()`, and add these lines of code instead:
-->

これで均等な間隔の点が得られました（図 13 の右側）。（線の最後に円が描かれていないことに注意。）線幅が変化するようなブラシのストロークを作成してみましょう。これを実現するには、[normal vector](https://en.wikipedia.org/w/index.php?title=Normal_vector)を利用します。図 14 はポリラインの上に描かれた法線を示していて、ポリラインに対して向き合った（垂直の）方向を向いています。図 15 のように、ポリラインに沿って全ての点で法線を描画することを想像してください。これはブラシに「太さ」を追加する一つの方法です。円を描画するコードを`draw()`の中からコメントアウトして、代わりに以下のコードを追加しましょう。

<!--
```cpp
    vector<ofVec3f> vertices = polyline.getVertices();
    float normalLength = 50;
    for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
        ofVec3f vertex = vertices[vertexIndex];  // Get the vertex
        ofVec3f normal = polyline.getNormalAtIndex(vertexIndex) * normalLength;  // Scale the normal
        ofDrawLine(vertex-normal/2, vertex+normal/2);  // Center the scaled normal around the vertex
    }
```
-->

```cpp
    vector<ofVec3f> vertices = polyline.getVertices();
    float normalLength = 50;
    for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
        ofVec3f vertex = vertices[vertexIndex];  // 頂点を取得
        ofVec3f normal = polyline.getNormalAtIndex(vertexIndex) * normalLength;  // 法線を拡縮
        ofDrawLine(vertex-normal/2, vertex+normal/2);  // 拡縮した法線を頂点を中心にセンタリング
    }
```

<!--
We are getting all of the vertices in our `ofPolyline`. But here, we are also using [`getNormalAtIndex`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getNormalAtIndex) which takes an index and returns an `ofVec3f` that represents the normal vector for the vertex at that index. We take that normal, scale it and then display it centered around the vertex. So, we have something like figure 14 (left), but we can also sample normals, using the function [`getNormalAtIndexInterpolated(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getNormalAtIndexInterpolated). So let's comment out the code we just wrote, and try sampling our normals evenly along the polyline:
-->

`ofPolyline`にある頂点全てを取得しています。しかしここでは[`getNormalAtIndex`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getNormalAtIndex)も利用していて、これは添字（インデックス）を受け取ってその添字の位置にある頂点に対応する法線を表す `ofVec3f`を返します。その法線を取得し、拡縮して頂点を中心にセンタリングして表示します。そうすると、図 14（左）のような状態になりますが、[`getNormalAtIndexInterpolated(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getNormalAtIndexInterpolated)関数を使って法線をサンプリングすることもできます。さっき書いたばかりのコードをコメントアウトして、ポリラインに沿って法線を均等にサンプリングしてみましょう。

<!--
![Figure 14: Drawing normals at the vertices of a polyline, without and with resampling points evenly](images/Figure14_PolylineNormals.png)
-->

![図 14: ポリラインの頂点の位置に法線を描画、点の均等な再サンプルの無しと有り](images/Figure14_PolylineNormals.png)

<!--
```cpp
float normalLength = 50;
for (int p=0; p<100; p+=10) {
    ofVec3f point = polyline.getPointAtPercent(p/100.0);
    float floatIndex = polyline.getIndexAtPercent(p/100.0);
    ofVec3f normal = polyline.getNormalAtIndexInterpolated(floatIndex) * normalLength;
    ofDrawLine(point-normal/2, point+normal/2);
}
```
-->

```cpp
float normalLength = 50;
for (int p=0; p<100; p+=10) {
    ofVec3f point = polyline.getPointAtPercent(p/100.0);
    float floatIndex = polyline.getIndexAtPercent(p/100.0);
    ofVec3f normal = polyline.getNormalAtIndexInterpolated(floatIndex) * normalLength;
    ofDrawLine(point-normal/2, point+normal/2);
}
```

<!--
We can get an evenly spaced point by using percents again, but `getNormalAtIndexInterpolated(...)` is asking for an index. Specifically, it is asking for a `floatIndex` which means that we can pass in 1.5 and the polyline will return a normal that lives halfway between the point at index 1 and halfway between the point at index 2. So we need to convert our percent, `p/100.0`, to a `floatIndex` using [`getIndexAtPercent(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline/#!show_getIndexAtPercent). Once we've done that, we'll have something like figure 14 (right).
-->

今度もパーセンテージによる均等な間隔の点が得られましたが、`getNormalAtIndexInterpolated(...)`は添字が必要です。具体的には、これは`floatIndex`という、1.5 を渡すとポリラインが添字の 1 と 2 の間の点の法線を返してくれるものを受け取ります。ですのでパーセントの`p/100.0`は[`getIndexAtPercent(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline/#!show_getIndexAtPercent)を使って`floatIndex`に変換する必要があります。これを行うと、図 14（右）のようになります。

<!--
Now we can pump up the number of normals in our drawing. Let's change our loop increment from `p+=10` to `p+=1`, change our loop condition from `p<100` to `p<500` and change our `p/100.0` lines of code to `p/500.0`. We might also want to use a transparent white for drawing these normals, so let's add `ofSetColor(255,100)` right before our loop. We will end up being able to draw ribbon lines, like figure 15.
-->

このあとはドローイングでの法線の数を増やしていくことができます。ループのインクリメントを`p+=10`から`p+=1`にして、ループの条件を`p<100`から`p<500`に変え、`p/100`のコード行を`p/500.0`に変更しましょう。法線を描画する白に透過を利用しても良いので、`ofSetColor(255,100)`をループの直前に追加しましょう。最終的に、図 15 のようなリボンのような線が描画できます。

<!--
![Figure 15: Drawing many many normals to fill out the polyline](images/Figure15_PolylineManyNormals.png)
-->

![図 15: ポリラインを埋めるように描画された非常に多くの法線](images/Figure15_PolylineManyNormals.png)

<!--
We've just added some thickness to our polylines. Now let's have a quick aside about tangents, the "opposite" of normals. These wonderful things are perpendicular to the normals that we just drew. So if we drew tangents along a perfectly straight line we wouldn't really see anything. The fun part comes when we draw tangents on a curved line, so let's see what that looks like. Same drill as before. Comment out the last code and add in the following:
-->

これでポリラインに太さが追加できました。それではちょっと余談で、法線の「真逆」の接線に触れましょう。この素晴らしきものはたった今描画したばかりの、法線に対して垂直です。ですのでもし完全な直線に接線を描画すると全く何も見えないでしょう。面白いのは曲線に接線を描画したときで、どんな風かみてみましょう。前と同じやりかたです。最後のコードをコメントアウトして下記を追加しましょう。

<!--
```cpp
vector<ofVec3f> vertices = polyline.getVertices();
float tangentLength = 80;
for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
    ofVec3f vertex = vertices[vertexIndex];
    ofVec3f tangent = polyline.getTangentAtIndex(vertexIndex) * tangentLength;
    ofDrawLine(vertex-tangent/2, vertex+tangent/2);
}
```
-->

```cpp
vector<ofVec3f> vertices = polyline.getVertices();
float tangentLength = 80;
for (int vertexIndex=0; vertexIndex<vertices.size(); vertexIndex++) {
    ofVec3f vertex = vertices[vertexIndex];
    ofVec3f tangent = polyline.getTangentAtIndex(vertexIndex) * tangentLength;
    ofDrawLine(vertex-tangent/2, vertex+tangent/2);
}
```

<!--
This should look very familiar except for [`getTangentAtIndex(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getTangentAtIndex) which is the equivalent of `getNormalAtIndex(...)` but for tangents. Not much happens for straight and slightly curved lines, however, sharply curved lines reveal the tangents figure 16 (left).
-->

これは[`getTangentAtIndex(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getTangentAtIndex)が`getNormalAtIndex(...)`と同様ながら接線のためのものであることを除けば見慣れたものです。直線や少しカーブした線では大したことは起きませんが、急にカーブした線では図 16（左）のような接線が現れます。
)

<!--
![Figure 16: Drawing tangents at vertices of polylines](images/Figure16_PolylineTangents.png)
-->

![図 16: ポリラインの頂点の部分への接線の描画](images/Figure16_PolylineTangents.png)

<!--
I'm sure you can guess what's next... drawing a whole bunch of tangents at evenly spaced locations (figure 16, right)! It's more fun that it sounds. [`getTangentAtIndexInterpolated(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getTangentAtIndexInterpolated) works like `getNormalAtIndexInterpolated(...)`. Same drill, comment out the last code, and add the following:
-->

次に何が起きるかは予想できるでしょう...接線を全ての均等な間隔の位置に描画するのです（図 16、右側）！聞くよりも楽しいです。[`getTangentAtIndexInterpolated(...)`](http://openframeworks.cc/documentation/graphics/ofPolyline.html#show_getTangentAtIndexInterpolated)が`getNormalAtIndexInterpolated(...)`のように機能します。同様のやり方で、最後のコードをコメントアウトし、以下を追加します。

<!--
```cpp
ofSetColor(255, 50);
float tangentLength = 300;
for (int p=0; p<500; p+=1) {
    ofVec3f point = polyline.getPointAtPercent(p/500.0);
    float floatIndex = polyline.getIndexAtPercent(p/500.0);
    ofVec3f tangent = polyline.getTangentAtIndexInterpolated(floatIndex) * tangentLength;
    ofDrawLine(point-tangent/2, point+tangent/2);
}
```
-->

```cpp
ofSetColor(255, 50);
float tangentLength = 300;
for (int p=0; p<500; p+=1) {
    ofVec3f point = polyline.getPointAtPercent(p/500.0);
    float floatIndex = polyline.getIndexAtPercent(p/500.0);
    ofVec3f tangent = polyline.getTangentAtIndexInterpolated(floatIndex) * tangentLength;
    ofDrawLine(point-tangent/2, point+tangent/2);
}
```

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_ii_b_Polyline_Brushes)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_b_Polyline_Brushes.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_ii_b_Polyline_Brushes)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_b_Polyline_Brushes.sketch)\]

<!--
**Extensions**
-->

**発展**

<!--
1. Try drawing shapes other than `ofDrawLine(...)` and `ofDrawCircle(...)` along your polylines. You could use your brush code from section 1.
2. The density of tangents or normals drawn is dependent on the length of the brush stroke. Try making it independent (hint: you may need to adjust your loop and use `getPerimeter()` to calculate the length).
3. Check out how to draw polygons using `ofPath` and try drawing a brush stroke that is a giant, closed shape.
-->

1. `ofDrawLine(...)`と`ofDrawCircle(...)`以外の図形をポリラインに沿って描画してみましょう。セクション 1 のブラシのコードを使うことも可能でしょう。
2. 描画する接線や法線の密度はブラシのストロークの長さに依存します。これを依存しないようにしてみましょう（ヒント：ループを調整し、`getPerimeter()`を使って長さを計算します。）
3. `ofPath`を使ってポリゴンを描画する方法を調べ、巨大な、閉じた図形を描画してみましょう。

<!--
#### Vector Graphics: Taking a Snapshot (Part 2)
-->

#### ベクターグラフィックス: スナップショットの撮影（パート 2）

<!--
Remember how we saved our drawings that we made with the basic shape brushes by doing a screen capture? Well, we can also save drawings as a PDF. A PDF stores the graphics as a series of geometric objects rather than as a series of pixel values. So, if we render out our polylines as a PDF, we can open it in a vector graphics editor (like [Inkscape](http://www.inkscape.org/en/) or Adobe Illustrator) and modify our polylines in all sorts of ways. For example, see figure 17 where I colored and blurred the polylines to create a glowing effect.
-->

画面キャプチャで基本的な形状のブラシで作成したドローイングを保存したやりかたを覚えていますか？ええ、ドローイングは PDF としても保存できます。PDF は一連のピクセル値としてではなく、図形オブジェクトとしてグラフィックを保存します。ですので、もしポリラインを PDF として保存すると、それはベクターグラフィックエディタ（[Inkscape](http://www.inkscape.org/en/) や Adobe Illustrator など）で開き、ポリラインをあらゆる方法で調整することができます。例として、図 17 でポリラインに色付けをしブラーをかけてグローエフェクトを作成しました。

<!--
Once we have a PDF, we could also use it to blow up our polyines to create a massive, high resolution print.
-->

PDF ができてしまえば、巨大な、高解像度印刷用にポリラインを引き延ばすこともできます。

<!--
To do any of this, we need to use [`ofBeginSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofBeginSaveScreenAsPDF) and [`ofEndSaveScreenAsPDF()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEndSaveScreenAsPDF). When we call `ofBeginSaveScreenAsPDF(...)`, any subsequent drawing commands will output to a PDF _instead of_ being drawn to the screen. `ofBeginSaveScreenAsPDF(...)` takes one required argument, a `string` that contains the desired filename for the PDF. (The PDF will be saved into `./bin/data/` unless you specify an alternate path). When we call `ofEndSaveScreenAsPDF()`, the PDF is saved and drawing commands begin outputting back to the screen.
-->

何をするにせよ、[`ofBeginSaveScreenAsPDF(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#!show_ofBeginSaveScreenAsPDF) および [`ofEndSaveScreenAsPDF()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofEndSaveScreenAsPDF)を使う必要があります。`ofBeginSaveScreenAsPDF(...)`を呼ぶと、後続の描画コマンドは画面に描画される _代わりに_ 、PDF に出力されます。`ofBeginSaveScreenAsPDF(...)`は一つ、PDF の希望ファイル名の`string`が必須の引数です。（PDF は別のパスを指定しなければ`./bin/data/`の中に保存されます）。`ofEndSaveScreenAsPDF()`を呼ぶと PDF は保存されて、描画コマンドはまた画面に出力されるようになります。

<!--
Let's use the polyline brush code from the last section to save a PDF. The way we saved a screenshot previously was to put `ofSaveScreen()` inside of `keyPressed(...)`. We can't do that here because `ofBeginSaveScreenAsPDF(...)` and `ofEndSaveScreenAsPDF()` need to be before and after (respectively) the drawing code. So we'll make use of a `bool` variable. Add `bool isSavingPDF` to the header (.h) file, and then modify your source code (.cpp) to look like this:
-->

最後のセクション、ポリラインブラシのプログラムコードを使って PDF を保存してみましょう。以前にスクリンショットを保存したやり方は、`keyPressed(...)`の中に`ofSaveScreen()`を書くというものでした。ここでそれは出来ませんが、なぜならば`ofBeginSaveScreenAsPDF(...)` と `ofEndSaveScreenAsPDF()`は、描画コードの（それぞれ）前と後ろに置く必要があるためです。したがって`bool`変数を利用します。`bool isSavingPDF`をヘッダ（.h）ファイルに追加して、ソースコード（.cpp）を以下のように編集します。

<!--
```cpp
void ofApp::setup(){
    // Setup code omitted for clarity...

    isSavingPDF = false;
}

void ofApp::draw(){
    // If isSavingPDF is true (i.e. the s key has been pressed), then
    // anything in between ofBeginSaveScreenAsPDF(...) and ofEndSaveScreenAsPDF()
    // is saved to the file.
    if (isSavingPDF) {
        ofBeginSaveScreenAsPDF("savedScreenshot_"+ofGetTimestampString()+".pdf");
    }

    // Drawing code omitted for clarity...

    // Finish saving the PDF and reset the isSavingPDF flag to false
    // Ending the PDF tells openFrameworks to resume drawing to the screen.
    if (isSavingPDF) {
        ofEndSaveScreenAsPDF();
        isSavingPDF = false;
    }
}

void ofApp::keyPressed(int key){
    if (key == 's') {
        // isSavingPDF is a flag that lets us know whether or not save a PDF
        isSavingPDF = true;
    }
}

```
-->

```cpp
void ofApp::setup(){
    // 簡単のためにセットアップコードは省略...

    isSavingPDF = false;
}

void ofApp::draw(){
    // isSavingPDF が true ならば（つまり s キーが押されたら）、
    // ofBeginSaveScreenAsPDF(...) と ofEndSaveScreenAsPDF()の間のものは全て
    // ファイルに保存されます。
    if (isSavingPDF) {
        ofBeginSaveScreenAsPDF("savedScreenshot_"+ofGetTimestampString()+".pdf");
    }

    // 簡単のために描画コードは省略...

    // PDF の保存を終了し、isSavingPDF フラグを false にリセット
    // PDF を終了すると openFrameworks は画面描画に戻ります。
    if (isSavingPDF) {
        ofEndSaveScreenAsPDF();
        isSavingPDF = false;
    }
}

void ofApp::keyPressed(int key){
    if (key == 's') {
        // isSavingPDF はPDFを保存するか否かのフラグ
        isSavingPDF = true;
    }
}

```

<!--
![Figure 17: Editing a saved PDF from openFrameworks in Illustrator](images/Figure17_EditingVectorGraphics.png)
-->

![図 17: openFrameworksから保存したPDFをIllustratorで編集する](images/Figure17_EditingVectorGraphics.png)

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/2_ii_c_Save_Vector_Graphics)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/2_ii_c_Save_Vector_Graphics.sketch)

<!--
## Moving The World
-->

## ワールド座標系の移動

<!--
We've been making brushes for a long time, so let's move onto something different: moving the world. By the world, I really just mean the coordinate system (though it sounds more exciting the other way).
-->

ブラシの作成を長いこと行ってきましたので、そろそろ違うこと、世界（ワールド）の移動に取り掛かりましょう。世界（ワールド）とは、実際には座標系を意味しています（though it sounds more exciting the other way）。

<!--
Whenever we call a drawing function, like `ofDrawRectangle(...)` for example, we pass in an `x` and `y` location at which we want our shape to be drawn. We know (0,0) to be the upper left pixel of our window, that the positive x direction is rightward across our window and that positive y direction is downward along our window (recall figure 1). We are about to violate this established knowledge.
-->

例えば`ofDrawRectangle(...)`のような描画関数を呼び出すときにはいつでも、図形を描画させたい場所の`x`と`y`座標を渡します。(0,0)はウインドウの左上のピクセルで、正の x の値はウインドウの右向き、正の y の値はウインドウの下向きでしたね（図 1 を思い出してください）。この定説を覆していきましょう。

<!--
Imagine that we have a piece of graphing paper in front of us. How would we draw a black rectangle at (5, 10) that is 5 units wide and 2 units high? We would probably grab a black pen, move our hands to (5, 10) on our graphing paper, and start filling in boxes? Pretty normal, but we could have also have kept our pen hand stationary, moved our paper 5 units left and 10 units down and then started filling in boxes. Seems odd, right? This is actually a powerful concept. With openFrameworks, we can move our coordinate system like this using `ofTranslate(...)`, but we can _also_ rotate and scale with `ofRotate(...)` and `ofScale(...)`. We will start with translating to cover our screen with stick figures, and then we will rotate and scale to create spiraling rectangles.
-->

目の前に方眼紙があると想像しましょう。(5,10)の場所に 5 単位の幅と 2 単位の高さの黒い四角形をどのように描画するでしょうか？おそらく黒いペンを手に取って、手を方眼紙の(5,10)に移動し、四角形を塗りつぶすでしょうか？至って普通ですが、ペンを持つ手を止めておいて、紙を 5 単位左、10 単位下に移動して四角形を塗りつぶすこともできるでしょう。変ですか？これは実際には協力な概念です。openFrameworks では、`ofTranslate(...)`を使ってこのように座標系を移動できますが、`ofRotate(...)`や`ofScale(...)`で回転や拡縮 _も_ 行うことができます。まず棒人間で画面を覆うように移動します。そうして回転とスケールで螺旋状の四角形を作成します。

<!--
### Translating: Stick Family
-->

### 移動：棒人間家族

<!--
[`ofTranslate`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofTranslate) first. `ofTranslate(...)` takes an x, a y and an optional z parameter, and then shifts the coordinate system by those specified values. Why do this? Create a new project and add this to our `draw()` function of our source file (.cpp):
-->

[`ofTranslate`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofTranslate)が最初です。`ofTranslate(...)`は x、y と任意の z パラメータを受け取り、座標系を指定された値だけ移動します。なぜこれをするか？新規プロジェクトを作成して、ソースファイル（.cpp）の`draw()`関数に以下を追加しましょう。

<!--
```cpp
// Draw the stick figure family
ofDrawCircle(30, 30, 30);
ofDrawRectangle(5, 70, 50, 100);
ofDrawCircle(95, 30, 30);
ofDrawRectangle(70, 70, 50, 100);
ofDrawCircle(45, 90, 15);
ofDrawRectangle(30, 110, 30, 60);
ofDrawCircle(80, 90, 15);
ofDrawRectangle(65, 110, 30, 60);
```
-->

```cpp
// 棒人間の家族を描画します
ofDrawCircle(30, 30, 30);
ofDrawRectangle(5, 70, 50, 100);
ofDrawCircle(95, 30, 30);
ofDrawRectangle(70, 70, 50, 100);
ofDrawCircle(45, 90, 15);
ofDrawRectangle(30, 110, 30, 60);
ofDrawCircle(80, 90, 15);
ofDrawRectangle(65, 110, 30, 60);
```

<!--
Draw a white background and color the shapes. You should end up with something like the leftmost portion of Figure 18.
-->

白い背景を描画して、図形を塗ります。最終的に図 18 の左端のようになるでしょう。

<!--
![Figure 18: Arranging a little stick figure family](images/Figure18_ArrangingTheFamily.png)
-->

![図 18: 小さな棒人間家族のアレンジArranging a little stick figure family](images/Figure18_ArrangingTheFamily.png)

<!--
What if, after figuring out where to put our shapes, we needed to draw them at a different spot on the screen, or to draw a row of copies? We _could_ change all the positions manually, or we could use `ofTranslate(...)` to move our coordinate system and leave the positions alone:
-->

どこに図形を描画するか決定したあとに、画面上の別の場所に描画するか、一連のコピーを描かなければいけないとしたらどうしますか？手動で全ての位置を変更することも _可能_ ですが、`ofTranslate(...)`を使って座標系を移動して位置はそのままに置いておくこともできます。

<!--
```cpp
// Loop and draw a row
for (int cols=0; cols<4; cols++) {

    // Draw the stick figure family (code omitted)

    ofTranslate(150, 0);
}
```
-->

```cpp
// ループして行を描画する
for (int cols=0; cols<4; cols++) {

    // 棒人間家族を描画（コードは省略）

    ofTranslate(150, 0);
}
```

<!--
So our original shapes are wrapped it in a loop with `ofTranslate(150, 0)`, which shifts our coordinate system to the left 150 pixels each time it executes. And we'll end up with figure 18 (second from left). Or something close to that, I randomized the colors in the figure - every family is different, right?
-->

元々の形状はループの中にまとめて`ofTranslate(150,0)`と一緒になっていますが、これは座標系を実行のたびに 150 ピクセルずつ左に移動させます。最終的には図 18（左から 2 番目）のようになります。または似ていますが、画像の色をランダムにしてみました。家族はみんな違いますよね？

<!--
If we wanted to create a grid of families, we will run into problems. After the first row of families, our coordinate system will have been moved quite far to the left. If we move our coordinate system up in order to start drawing our second row, we will end up drawing off the screen in a diagonal. It would look like figure 18 (third from left).
-->

家族をグリッド上に置こうとすると、問題に遭遇します。一行目を描画し終わると、座標系は左に移動しすぎています。2 行目を描画するために座標系を上に移動すると、対角線上の画面外に描画してしまうでしょう。これは図 18（左から 3 番目）のような状態です。

<!--
So what we need is to reset the coordinate system using [`ofPushMatrix()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofPushMatrix) and [`ofPopMatrix()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofPopMatrix). `ofPushMatrix()` saves the current coordinate system and `ofPopMatrix()` returns us to the last saved coordinate system. These functions have the word matrix in them because openFrameworks stores all of our combined rotations, translations and scalings in a single matrix. So we can use these new functions like this:
-->

ですので[`ofPushMatrix()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofPushMatrix)と[`ofPopMatrix()`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofPopMatrix)を使って座標系をリセットすることが必要です。`ofPushMatrix()`は現在の座標系を保存して、`ofPopMatrix()`は最後に保存した座標系を返してくれます。これらの関数には matrix という単語が入っていて、なぜならば openFrameworks は回転、移動、拡縮小を全て結合して一つの行列で保持しているからです。これらの新しい関数は以下のように使用できます。

<!--
```cpp
    for (int rows=0; rows<10; rows++) {
        ofPushMatrix(); // Save the coordinate system before we shift it horizontally

        // It is often helpful to indent any code in-between push and pop matrix for readability

        // Loop and draw a row (code omitted)

        ofPopMatrix(); // Return to the coordinate system before we shifted it horizontally
        ofTranslate(0, 200);
    }
```
-->

```cpp
    for (int rows=0; rows<10; rows++) {
        ofPushMatrix(); // 水平に移動する前に座標系を保存します

        // 可読性のために、行列のpushとpopの間のコードをインデントしておくと良いかもしれません

        // ループして一行描画します（コード省略）

        ofPopMatrix(); // 水平に移動する前の座標系に戻る
        ofTranslate(0, 200);
    }
```

<!--
And we should end up with a grid. See figure 18, right. (I used `ofScale` to jam many in one image.) Or if you hate grids, we can make a mess of a crowd using random rotations and translations, figure 19.
-->

最終的にグリッド上になります。図 18 の右側をご覧ください。（`ofScale`を使って大勢を一つの画像に詰め込みました。）グリッドが嫌ならば、ランダムな回転や移動を使って図 19 のようなぐちゃぐちゃの群衆にできます。

<!--
![Figure 19: A crowd](images/Figure19_Crowd.png)
-->

![図 19: 群衆](images/Figure19_Crowd.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/3_i_Translating_Stick_Family)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_i_Translating_Stick_Family.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/3_i_Translating_Stick_Family)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_i_Translating_Stick_Family.sketch)\]

<!--
### Rotating and Scaling: Spiraling Rectangles
-->

### 回転と拡縮: 渦巻く四角形

<!--
Onto `ofScale(...)` and `ofRotate(...)`! Let's create a new project where rotating and scaling rectangles to get something like figure 20.
-->

`ofScale(...)`と`ofRotate(...)`を続けます！新規プロジェクトを作成して回転と拡縮で図 20 のような形にします。

<!--
![Figure 20: Drawing a series of spiraling rectangles](images/Figure20_SpiralingRectangles.png)
-->

![図 20: 渦巻く一連の四角形の描画](images/Figure20_SpiralingRectangles.png)

<!--
Before knowing about `ofRotate(...)`, we couldn't have drawn a rotated rectangle with `ofDrawRectangle(...)`. [`ofRotate(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofRotate) takes an angle (in degrees) and rotates our coordinate system around the current origin. Let's attempt a rotated rectangle:
-->

`ofRotate(...)`について理解せずに`ofDrawRectangle(...)`で回転した四角形を描画することはできません。[`ofRotate(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofRotate)は角度（degree）を受け取って現在の原点を中心に座標系を回転させます。四角形の回転を試してみましょう。

<!--
```cpp
ofBackground(255);
ofPushMatrix();
    // Original rectangle in blue
    ofSetColor(0, 0, 255);
    ofDrawRectangle(500, 200, 200, 200);

    // Rotated rectangle in red
    ofRotate(45);
    ofSetColor(255, 0, 0);
    ofDrawRectangle(500, 200, 200, 200);
ofPopMatrix();
```
-->

```cpp
ofBackground(255);
ofPushMatrix();
    // 元の四角形を青色にします
    ofSetColor(0, 0, 255);
    ofDrawRectangle(500, 200, 200, 200);

    // 回転した四角形は赤色にします
    ofRotate(45);
    ofSetColor(255, 0, 0);
    ofDrawRectangle(500, 200, 200, 200);
ofPopMatrix();
```

<!--
Hmm, not quite right (figure 21, left). `ofRotate(...)` rotates around the current origin, the top left corner of the screen. To rotate in place, we need `ofTranslate(...)` to move the origin to our rectangle _before_ we rotate. Add `ofTranslate(500, 200)` before rotating (figure 21, second from left). Now we are rotating around the upper left corner of the rectangle. The easiest way to rotate the rectangle around its center is to use `ofSetRectMode(OF_RECTMODE_CENTER)` draw the center at (500, 200). Do that, and we finally get figure 21, third from left.
-->

うーむ、正しくありませんね（図 21、左側）。`ofRotate(...)`は現在の原点を中心に回転しますが、これは画面の左上の角です。その場で回転させるには、`ofTranslate(...)`で四角形を回転する _前に_ 原点を移動させる必要があります。`ofTranslate(500, 200)`を回転の前に追加しましょう（図 21、左から 2 つ目）。今は四角形の左上の角を中心に回転させています。中心を軸に回転させるのに最も簡単なのは、`ofSetRectMode(OF_RECTMODE_CENTER)`を使って(500, 200)に中心を描画します。これをすると、図 21 の左から 3 番目のようになります。

<!--
![Figure 21: Steps along the way to rotating and scaling a rectangle in place](images/Figure21_CoordSystemManipulations.png)
-->

![図 21: 順を追ってその場で四角形を回転および拡縮する](images/Figure21_CoordSystemManipulations.png)

<!--
Push, translate, rotate, pop - no problem. Only thing left is [`ofScale(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofScale). It takes two arguments: the desired scaling in x and y directions (and an optional z scaling). Applying scaling to our rectangles:
-->

プッシュ、移動、回転、ポップ。問題ありませんね。残すは[`ofScale(...)`](http://openframeworks.cc/documentation/graphics/ofGraphics.html#show_ofScale)です。これは 2 つの引数、望みの x と y 方向（それと任意の z 方向）の拡縮率を取ります。スケーリングを四角形に適用しましょう。

<!--
```cpp
ofSetRectMode(OF_RECTMODE_CENTER);
ofBackground(255);

ofPushMatrix();
    // Original rectangle in blue
    ofSetColor(0, 0, 255);
    ofDrawRectangle(500, 200, 200, 200);

    // Scaled down rectangle in red
    ofTranslate(500, 200);
    ofScale(0.5, 0.5);  // We are only working in x and y, so let's leave the z scale at its default (1.0)
    ofSetColor(255, 0, 0);
    ofDrawRectangle(0, 0, 200, 200);
ofPopMatrix();
```
-->

```cpp
ofSetRectMode(OF_RECTMODE_CENTER);
ofBackground(255);

ofPushMatrix();
    // 元の四角形を青色にします
    ofSetColor(0, 0, 255);
    ofDrawRectangle(500, 200, 200, 200);

    // 縮小された四角形を赤色にします
    ofTranslate(500, 200);
    ofScale(0.5, 0.5);  // xとyだけを扱っていますので、zはデフォルト（1.0)のままにしておきます
    ofSetColor(255, 0, 0);
    ofDrawRectangle(0, 0, 200, 200);
ofPopMatrix();
```

<!--
We'll run into the same issues that we ran into with rotation and centering. The solution is the same - translating before scaling and using `OF_RECTMODE_CENTER`. Example scaling shown in figure 21 (right).
-->

ここでも回転とセンタリングで遭遇したのと同じ問題が起きます。解決策も同じで、拡縮の前に`OF_RECTMODE_CENTER`を使って移動を行います。縮小の例が図 21（右側）です。

<!--
Now we can make trippy rectangles. Start a new project. The idea is really simple, we are going to draw a rectangle at the center of the screen, scale, rotate, draw a rectangle, repeat and repeat. Add the following to our `draw()` function:
-->

これで我々はトリップしたような四角形を作ることができます。新規プロジェクトを開始します。概念は非常にシンプルで、四角形を画面の中央に描画し、スケーリングして、回転、四角形を描画、これを繰り返します。下記を`draw()`関数に追加しましょう。

<!--
```cpp
ofBackground(255);

ofSetRectMode(OF_RECTMODE_CENTER);
ofSetColor(0);
ofNoFill();
ofPushMatrix();
    ofTranslate(ofGetWidth()/2, ofGetHeight()/2);  // Translate to the center of the screen
    for (int i=0; i<100; i++) {
        ofScale(1.1, 1.1);
        ofRotate(5);
        ofDrawRectangle(0, 0, 50, 50);
    }
ofPopMatrix();
```
-->

```cpp
ofBackground(255);

ofSetRectMode(OF_RECTMODE_CENTER);
ofSetColor(0);
ofNoFill();
ofPushMatrix();
    ofTranslate(ofGetWidth()/2, ofGetHeight()/2);  // 画面の中央まで移動する
    for (int i=0; i<100; i++) {
        ofScale(1.1, 1.1);
        ofRotate(5);
        ofDrawRectangle(0, 0, 50, 50);
    }
ofPopMatrix();
```

<!--
That's it (figure 20). We can play with the scaling, rotation, size of the rectangle, etc. Three lines of code will add some life to our rectangles and cause them to coil and uncoil over time. Put these in the place of `ofRotate(5)`:
-->

これがそれです（図 20）。拡縮率、回転、四角形のサイズ等を色々試すことができます。3 行のコードを追加すると四角形に新たな生命を与え、時間の経過と共に渦を巻いたり解いたりするようになります。以下を`ofRotate(5)`の場所に書いてみましょう。

<!--
```cpp
// Noise is a topic that deserves a section in a book unto itself
// Check out Section 1.6 of "The Nature of Code" for a good explanation
// http://natureofcode.com/book/introduction/
float time = ofGetElapsedTimef();
float timeScale = 0.5;
float noise = ofSignedNoise(time * timeScale) * 20.0;
ofRotate(noise);
```
-->

```cpp
// ノイズはそれ自体で一つの章を割くべきトピックです
// セクション1.6の「プログラムコードの性質（The Nature of Code）」に良い説明があります。
// http://natureofcode.com/book/introduction/
float time = ofGetElapsedTimef();
float timeScale = 0.5;
float noise = ofSignedNoise(time * timeScale) * 20.0;
ofRotate(noise);
```

<!--
Next, we can create a visual smear ("trail effect") as it rotates if we will turn off the background automatic clearing and partially erase the screen before drawing again. To do this add a few things to `setup()`:
-->

次に、背景の自動消去を無効化して再描画の前に部分的に消去することで視覚的な染み（トレイル・エフェクト）を回転に合わせて作り出すことができます。これをするには`setup()`に幾つか追加します。

<!--
```cpp
ofSetBackgroundAuto(false);
ofEnableAlphaBlending(); // Remember if we are using transparency, we need to let openFrameworks know
ofBackground(255);
```
-->

```cpp
ofSetBackgroundAuto(false);
ofEnableAlphaBlending(); // 透明度を使う場合は、openFrameworksに知らせる必要があります。
ofBackground(255);
```

<!--
Delete `ofBackground(255)` from our `draw()` function. Then, add this to the beginning of our `draw()` function:
-->

`ofBackground(255)`を`draw()`関数から削除します。それから、これを`draw()`関数の最初に追加します。

<!--
```cpp
float clearAlpha = 100;
ofSetColor(255, clearAlpha);
ofSetRectMode(OF_RECTMODE_CORNER);
ofFill();
ofDrawRectangle(0, 0, ofGetWidth(), ofGetHeight());  // ofBackground doesn't work with alpha, so draw a transparent rect
```
-->

```cpp
float clearAlpha = 100;
ofSetColor(255, clearAlpha);
ofSetRectMode(OF_RECTMODE_CORNER);
ofFill();
ofDrawRectangle(0, 0, ofGetWidth(), ofGetHeight());  // ofBackground はアルファ値を扱えないので、透明の四角形を描画します。
```

<!--
Pretty hypnotizing? If we turn up the `clearAlpha`, we will turn down the smear. If we turn down the `clearAlpha`, we will turn up the smear.
-->

とても魅力的でしょう？`clearAlpha`の値を上げると、不鮮明さを減らすことができます。`clearAlpha`の値を下げると、不鮮明さは大きくなります。

<!--
Now we've got two parameters that drastically change the visual experience of our spirals, specifically: `timeScale` of noise and `clearAlpha` of the trail effect. Instead of manually tweaking their values in the code, we can use the mouse position to independently control the values during run time. Horizontal position can adjust the `clearAlpha` while vertical position can adjust the `timeScale`. This type of exploration of parameter settings is super important (especially when making generative graphics), and using the mouse is handy if we've got one or two parameters to explore.
-->

これで我々は、螺旋の視覚体験をドラスティックに変化させる具体的なパラメータ、ノイズの`timeScale`とトレイル・エフェクトの`clearAlpha`を手に入れました。手動でこれらの値をコードでいじるのではなく、それぞれ実行時にマウスの位置で制御することができます。水平位置で`clearAlpha`、垂直位置で`timeScale`を調整できます。このタイプのパラメタの調整は（特にジェネラティブ・グラフィックスの作成時には）非常に重要で、マウス位置の利用は調整したいパラメタが一つか二つの時には便利です。

<!--
[`mouseMoved(int x, int y )`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_mouseMoved) runs anytime the mouse moves (in our app). We can use this function to change our parameters. Like with `mousePressed(...)`, if you are using project generator, you'll find this with your mouse functions in your `.cpp` file. If you are using ofSketch, you might not see this function, but it's easy to add. See the [ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling.sketch) for this section.
-->

[`mouseMoved(int x, int y )`](http://openframeworks.cc/documentation/application/ofBaseApp.html#!show_mouseMoved)は（アプリ中で）マウスが移動した際に常に実行されます。この関数をパラメータを変化させるのに利用できます。`mousePressed(...)`と同様に、project generator を使っているならば`.cpp`ファイルのマウス関数の中に見つかるでしょう。ofSketch を利用しているならばこの関数はないでしょうが、簡単に追加できます。このセクションの[ofSketch file](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling.sketch)をご覧ください。

<!--
Before we use this function, we need to make our parameters global in their scope. Delete the code that defines `timeScale` and `clearAlpha` locally in `draw()` and add them to the header. Initialize the values in `setup()` to `100` and `0.5` respectively. Then add these to `mouseMoved(...)`:
-->

<!--
```cpp
clearAlpha = ofMap(x, 0, ofGetWidth(), 0, 255);  // clearAlpha goes from 0 to 255 as the mouse moves from left to right
timeScale = ofMap(y, 0, ofGetHeight(), 0, 1);  // timeScale goes from 0 to 1 as the mouse moves from top to bottom
```
-->

```cpp
clearAlpha = ofMap(x, 0, ofGetWidth(), 0, 255);  // clearAlpha はマウスが左から右に動くのに合わせて 0 から 255 まで変化します
timeScale = ofMap(y, 0, ofGetHeight(), 0, 1);  // timeScale はマウスが上から下に動くのに合わせて 0 から 1 まで変化します
```

<!--
One last extension. We can slowly flip the background and rectangle colors, by adding this to the top of `draw()`:
-->

最後の拡張です。`draw()`の最初に以下を追加することで背景と四角形の色をゆっくりと反転させることができます。

<!--
```cpp
ofColor darkColor(0,0,0,255);  // Opaque black
ofColor lightColor(255,255,255,255);  // Opaque white
float time = ofGetElapsedTimef();  // Time in seconds
float percent = ofMap(cos(time/2.0), -1, 1, 0, 1);  // Create a value that oscillates between 0 to 1
ofColor bgColor = darkColor;  // Color for the transparent rectangle we use to clear the screen
bgColor.lerp(lightColor, percent);  // This modifies our color "in place", check out the documentation page
bgColor.a = clearAlpha;  // Our initial colors were opaque, but our rectangle needs to be transparent
ofColor fgColor = lightColor;  // Color for the rectangle outlines
fgColor.lerp(darkColor, percent);  // Modifies color in place
```
-->

```cpp
ofColor darkColor(0,0,0,255);  // 不透明の黒
ofColor lightColor(255,255,255,255);  // 不透明の白
float time = ofGetElapsedTimef();  // 時間を秒で
float percent = ofMap(cos(time/2.0), -1, 1, 0, 1);  // 0から1の間で変動する値を作る
ofColor bgColor = darkColor;  // 画面を消去するための透明な四角形用の色
bgColor.lerp(lightColor, percent);  // これは色を「その場で」変更します。ドキュメントページを参照
bgColor.a = clearAlpha;  // 初期の色は不透明ですが、四角形の色は透過な必要があります
ofColor fgColor = lightColor;  // 四角形の輪郭用の色
fgColor.lerp(darkColor, percent);  // その場で色を変更する
```

<!--
Now use `bgColor` for the transparent rectangle we draw on the screen and `fgColor` for the rectangle outlines to get figure 22.
-->

`bgColor`を透過な四角形を画面に描画するために使い、`fgColor`を四角形の輪郭の描画に使うと、図 22 が得られます。

<!--
![Figure 22: A single frame from animated spiraling rectangles where the contrast reverses over time](images/Figure22_ContrastReversingSpiral.png)
-->

![図 22: 時間経過につれてコントラストが反転する、螺旋状のアニメーションをする四角形の1フレーム](images/Figure22_ContrastReversingSpiral.png)

<!--
\[[Source code for this section](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling)\]

\[[ofSketch file for this section](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling.sketch)\]
-->

\[[このセクションのソースコード](https://github.com/openframeworks/ofBook/tree/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling)\]

\[[このセクションの ofSketch ファイル](https://github.com/openframeworks/ofBook/blob/master/chapters/intro_to_graphics/code/3_ii_Rotating_and_Scaling.sketch)\]

<!--
**Extensions**
-->

**発展**

<!--
1. Pass in a third parameter, `z`, into `ofTranslate(...)` and `ofScale(...)` or rotate around the x and y axes with `ofRotate(...)`.
2. Capture animated works using an addon called [ofxVideoRecorder](https://github.com/timscaffidi/ofxVideoRecorder). If you are using Windows, like me, that won't work for you, so try screen capture software (like fraps) or saving out a series of images using `ofSaveScreen(...)` and using them to create a GIF or movie with your preferred tools (Photoshop, [ffmpeg](https://ffmpeg.org/), [ImageMagick](http://imagemagick.org/) etc.)
-->

1. `ofTranslate(...)`と`ofScale(...)`の 3 番目のパラメータの`z`を渡すか`ofRotate(...)`で x および y 軸を中心に回転させてみましょう。
2. [ofxVideoRecorder](https://github.com/timscaffidi/ofxVideoRecorder)というアドオンでアニメーション作品をキャプチャしてみましょう。私のように Windows を利用しているならばこれは機能しないでしょうから、画面キャプチャソフト（fraps のような）を試すか、`ofSaveScreen(....)`で一連の画像を保存して、任意のツール（Photoshop、[ffmpeg](https://ffmpeg.org/)、[ImageMagick](http://imagemagick.org/)等）で GIF や動画を作成してみましょう。

<!--
## Next Steps
-->

## 次のステップ

<!--
Congratulations on surviving the chapter :). You covered a lot of ground and (hopefully) made some fun things along the way - which you should share on the [forums](http://forum.openframeworks.cc/)!
-->

このチャプターの最後まで到達されて、おめでとうございます:)。多くの基礎をカバーでき、（望むらくは）過程において[フォーラム](http://forum.openframeworks.cc/)に投稿できるような楽しい作品を多く作成したでしょう。

<!--
If you are looking to learn more about graphics in openFrameworks, definitely continue on to _Advanced Graphics_ chapter to dive into more advanced graphical features. You can also check out these three tutorials: [Basics of Generating Meshes from an Image](http://openframeworks.cc/tutorials/graphics/generativemesh.html), for a gentle introduction to meshes; [Basics of OpenGL](http://openframeworks.cc/tutorials/graphics/opengl.html), for a comprehensive look at graphics that helps explain what is happening under the hood of openFrameworks; and [Introducing Shaders](http://openframeworks.cc/tutorials/graphics/shaders.html), for a great way to start programming with your graphical processing unit (GPU).
-->

もしあなた openFrameworks でのグラフィックスについてより学びたいと考えたなら、ぜひ続けて _Advanced Graphics_ の章へ行き、より先進的なグラフィックス機能に取り組んでください。下記の 3 つのチュートリアルをチェックしても良いでしょう。メッシュの親切な導入には[Basics of Generating Meshes from an Image](http://openframeworks.cc/tutorials/graphics/generativemesh.html)、openFrameworks の背後で何が行われているかを説明するためにグラフィックスについて包括的な見方については[Basics of OpenGL](http://openframeworks.cc/tutorials/graphics/opengl.html)、GPU プログラミングを開始する素晴らしい方法として[Introducing Shaders](http://openframeworks.cc/tutorials/graphics/shaders.html)。
