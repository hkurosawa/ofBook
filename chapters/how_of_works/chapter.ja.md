# openFrameworksの動作
## よくOFのコードで使われるパターンの簡単な説明

*by [Arturo Castro](http://arturocastro.net)*

openFrameworksはオープンソースのC++ツールキットであり、実験のためのシンプルで直感的な枠組みを提供することでクリエイティブな活動を手助けしています。このツールキットは汎用的な糊のように機能するようにデザインされており、いくつかの一般的に利用されるライブラリ群をラップしています。

openFrameworksが使うのは少ないパターンであり、どのように動作するか理解しやすくなっています。これらのパターンがどんなものかを一度理解すれば、openFrameworksでのどんな機能でも利用することが容易になるでしょう。

もしあなたがOFに貢献している開発者ならば、このドキュメントはあなたのクラスがopenFrameworksのその他の部分と一貫した振る舞いをするにはどのようにコーディングすれば良いかを知るために使えるでしょう。

## setup, update, draw

openFramwowksの大部分の機能がこのパータンを使って機能しています。全てのofAppのサンプルにおいてもsetup、updateそしてdrawメソッドがあります。

### setup()

setupメソッドはアプリケーションの開始時点で一度だけ呼ばれて、通常は `ofApp.h`で宣言されているオブジェクトや変数を初期化するために使われます。

__ofApp.h__

~~~~{.cpp}
ofVideoPlayer player;
int counter;
~~~~

__ofApp.cpp__

~~~~{.cpp}
void ofApp::setup(){
    player.loadMovie("movie.mov");
    counter = 0;
}
~~~~

C++では変数はデフォルトで初期化されないため、初期化は非常に重要なことです。例えば、もし`counter = 0;`を実行しなければ、`counter`はどんな値の可能性もあるのです。


### update/draw()

updateとdrawは、無限ループの中でこの順番でアプリケーションが終了されるまで呼び出されます。 

updateはアプリケーションの状態を更新するために使われることを意図しており、何らかの必要な計算を実行したりビデオプレーヤやキャプチャ（grabber）またはコンピュータビジョン解析などといった行なっているであろう他のオブジェクトの更新を行います。

drawでは画面描画を行います。


__ofApp.h__

~~~~{.cpp}
float x;
~~~~

__ofApp.cpp__

~~~~{.cpp}
void ofApp::setup(){
    x = 0;
}

void ofApp::update(){
    x++;
}

void ofApp::draw(){
    ofDrawCircle(x,120,30);
}
~~~~

これはy=120の位置に円を描画して画面の左から右に動かそうとしています。

## クラス

openFrameworksの大部分はクラスで構成されています。クラスには3つのタイプがあります。

### ユーティリティクラス

これは何かを実行するクラスです。これはofVideoGrabber、ofVideoPlayer、ofSoundPlayer、ofImage…といったクラスです。これらのクラスの大部分はsetup/update/drawパターンを使って動作しています。もちろんいくつかにおいてdrawは意味を成しません。例えばofSoundPlayerはdrawメソッドを持っていません。

これらのクラスは共有ポインタパターンにも準拠しています。これは、それらがコピーされる際、そのコピーは実際にはシャローコピー（shallow copy、浅いコピー）と呼ばれるものだということです。シャローコピーは単なるオブジェクトの参照であって、その内容物のコピーではありません。

例えば、ビデオプレーヤをコピーしてコピーをなんらか変更した場合、それはオリジナルも変更しています。

__ofApp.h__

~~~~{.cpp}
ofVideoPlayer player;
~~~~

__ofApp.cpp__

~~~~{.cpp}
void ofApp::update(){
    ofVideoPlayer player2 = player;
    player2.setFrame(100);
}
~~~~

これは、実際にはplayerとplayer2は同じオブジェクトの参照であるため、両方のプレーヤのカレントフレームが100に変更されています。


### データコンテナ

このクラスはデータを保持していて、そのデータの何らかの操作を行います。このクラスの例はofPixelやofBufferです。

このクラスはallocate/loadDataパターンに従っています。allocateはコンテナにメモリを確保して、その中にloadDataを使ってデータを入れていきます。これらの関数の名前はクラスによって変わりますが機能としては同じです。このクラスをコピーするとディープコピー（深いコピー）を作成します。これはコピーがオリジナルと同じ内容を持った全く新規のオブジェクトであり、コピーを変更してもオリジナルには影響しないということです。

__ofApp.h__

~~~~{.cpp}
ofPixels pixels1, pixels2;
ofTexture tex1, tex2;
~~~~

__ofApp.cpp__

~~~~{.cpp}
void ofApp::setup(){
    pixels1.allocate(640,480,OF_IMAGE_COLOR);
    pixels1.set(0);
    pixels2 = pixels1;
    pixels2.setColor(10,10,ofColor(255,255,255));

    tex1.allocate(640,480,GL_RGB);
    tex2.allocate(640,480,GL_RGB);
    tex1.loadData(pixels1);
    tex2.loadData(pixels2);
}

void ofApp::draw(){
    tex1.draw(0,0);
    tex2.draw(660,0);
}
~~~~

これは画面の左側に真っ黒な画像、右側には10,10の位置に白いピクセルのある黒い画像を描画します。`pixels2 = pixels1`を実行した場合、`pixels2`には`pixels1`と同じサイズとチャンネル数が割り当てられ、 `pixels1`のデータは`pixels2`にコピーされます。

### GLデータコンテナ

GLデータコンテナは、データコンテナの特殊なケースです。これの機能はデータコンテナのそれと非常に似通っていて、allocate/loadDataパターンにも従っています。これにはofTexture、ofFboやofVboMeshといったものがあります。これらは全てglフォルダーの中にありますが、glフォルダーの中身全てがデータコンテナではありません。ofShaderやofLightはGLユーティリティクラスであり、その他のユーティリティクラスと同様に機能します。

GLデータコンテナとその他のデータコンテナの主な違いは、GLデータコンテナがシャローコピーパタンに従っているということです。これの主な理由はパフォーマンスで、GPUの中でリソースのコピーを作成することは通常遅く、デフォルトでコピーは行いたくないためです。

例:

__ofApp.h__

~~~~{.cpp}
ofTexture tex1, tex2;
~~~~

__ofApp.cpp__

~~~~{.cpp}
void ofApp::setup(){
    tex1.allocate(640,480,GL_RGB);
    ofPixels pixels;
    pixels.allocate(640,480,OF_IMAGE_COLOR);
    pixels.set(0);
    tex1.loadData(pixels);
    tex2 = tex1;
    pixels.setColor(10,10,ofColor(255,255,255));
    tex2.loadData(pixels);
}

void ofApp::draw(){
    tex1.draw(0,0);
    tex2.draw(660,0);
}
~~~~

これは10,10の位置に白いピクセルがある黒い四角形を画面の左右両方に描画します。この理由は、このケースではGLリソースをコピーしていて、これは元のテクスチャのテクスチャIDに対する参照に過ぎず、完全なコピーではないためで、つまりこれを変更するとオリジナルも変更していることになるのです。

### データ型

これはopenFrameworksにおける`ofRectangle`、`ofVec3f`や`ofMatrix4x4`といった型を表現しています。

## 関数

openFrameworksの機能にはプレーンなCの関数として提供されているものもあります。これは通常、`ofToString()`、`ofRandom()`、`ofDrawBitmapString()`といった便利関数や、`ofDrawCircle()`、`ofDrawRectangle()`といった単純な描画関数です。
