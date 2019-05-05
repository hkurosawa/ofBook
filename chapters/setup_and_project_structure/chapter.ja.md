<!--
# oF structure
-->

# oF の構造

<!--
_by [Roy Macdonald](https://github.com/roymacdonald/)_
-->

<!--
Let's get into openFrameworks (I'll refer to it as oF from now on). The philosophy chapter talks about oF in a very abstract and conceptual manner, which is really useful for understanding the design of the oF environment. Now, let's take a look at what the oF download looks like.
-->

さて、openFrameworks を学んでいきましょう（これからは oF と呼んでいきます）。哲学の章は oF について抽象的かつ概念的な方法でお話しましたが、これは oF 環境のデザインについて理解するには非常に有用でした。今度は oF のダウンロードがどんな感じか見ていきましょう。

<!--
I have found it very useful to explain oF by making analogies to cooking. Coding and cooking have a lot of things in common, and most people are familiar with the act of cooking. In this chapter, I'll be drawing connections between processes and terminology in cooking and oF.
-->

私は料理との対比で oF を説明していくことがとても有効であることに気づきました。コーディングと料理はたくさんの共通点があって、ほとんどの人は料理の作業について慣れ親しんでいます。この章では、料理と oF でのプロセスや用語の関連付けをしていきます。

<!--
## First things first
-->

## 何はともあれ

<!--
You need to download the oF version and the [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment "Wikipedia article on IDE") (Integrated Development Environment) that suits your platform. The IDE is a piece of software that will let you write, compile, run and debug the code you write. It is "integrated" because it uses other pieces of software to do each of the mentioned tasks. You can run your code without using the IDE, but the IDE will make your programming life much easier.
-->

あなたのプラットフォームに対応した oF のバージョンと[IDE](https://en.wikipedia.org/wiki/Integrated_development_environment "IDEのWikipedia記事") (統合開発環境)をダウンロードする必要があります。IDE はあなたがコードを書き、コンパイルし、実行して実行できるソフトウェアの一つです。それは上記のタスクのそれぞれを実行するために他のソフトウェアを利用するので「統合されている」のです。あなたは IDE を利用せずにコードを実行できますが、IDE であなたのプログラミング人生はずっと楽になるでしょう。

<!--
Go to [http://openframeworks.cc/download](http://openframeworks.cc/download "Download openFrameworks!") and download the version that you need. By the side of each available version, you will find a link to download the matching IDE and how to install it.
-->

[http://openframeworks.cc/download](http://openframeworks.cc/download "openFrameworksをダウンロードする！")に行き、必要なバージョンをダウンロードします。それぞれの入手可能なバージョンの横に、対応する IDE のダウンロードリンクとインストール方法があります。

<!--
## Welcome to your new kitchen
-->

### あなたの新しいキッチン

<!--
### IDE
-->

### IDE

<!--
As said before, the _Integrated Development Environment_, IDE, is the application you will be using to build your oF projects. It will let you write code, compile (bake it), test it and debug it (find out what is giving you a problem, if there is any, and fix it). There are several different IDEs, at least one for each platform you might be utilizing.
-->

前述したように、_統合開発環境_ つまり IDE は、oF プロジェクトをビルドするために利用するアプリケーションです。これであなたはコーディング、コンパイル（焼き上げ）、テストしてデバッグ（問題があるとして、なにが原因かを見つけて修正）します。いくつかの異なる IDE がありますが、あなたのプラットフォームで少なくとも一つは利用可能でしょう。

<!--
The IDE is your new kitchen, where you'll find all the tools to cook incredible stuff. Yet there are a lot of different kitchen brands, just like IDEs. All do the same basic things but might be laid out and named in a slightly different way. If you know how to use one, you can use any other. For clarification, I will go through each IDE and show where you will find the most used commands, controls, and settings. Only read the IDE you are going to use.
-->

IDE はあなたの真新しいキッチンで、そこであなたが驚くべきものを料理するためのツールがあります。キッチンのブランドはたくさんありますが、IDE も同様です。基本的なことは全て同様に行えますが、レイアウトや名前は微妙に異なります。一つの使い方を覚えれば、他のものも利用できるでしょう。説明のためにそれぞれの IDE を見て、最も利用されるコマンドやコントロール、設定がどこにあるかをみてみましょう。利用予定の IDE だけ見てみてください。

<!--
All IDEs have a similar interface:
-->

全ての IDE は似たインターフェースを持っています。

<!--
![Abstract IDE interface](images/IDE_Interface.jpg "Abstract IDE interface")
-->

![概念的なIDEインターフェース](images/IDE_Interface.jpg "概念的なIDEインターフェース")

<!--
- Toolbar and Run Button: In the tool bar you'll find several useful buttons, such as open, save, save all, et cetera. The "run" button is very important. Usually, it is labeled with a triangle pointing to the right, like the "play" button. When you press it, your code will compile and if no problems are encountered it will automatically run your code. Hence this is a frequently used button.
- File selector and project navigator area: Here you will see your project and the files associated with it. Usually, it is displayed as a hierarchically ordered list of files. Here you'll find all the oF library files, as well as the files that are particular to your project.
- Editing area: When you open a file in the project navigation area, usually by double-clicking it, it should open in the editing area. This looks just like any regular text-editing software and behaves much the same.
- Console: This is where your app, when running, outputs messages. These messages are really useful for debugging. You can print text messages to the console using the `cout` command or [`ofLog(...)`](http://openframeworks.cc/documentation/utils/ofLog.html "ofLog Documentation Page") function.
-->

- ツールバーと実行ボタン：ツールバーにはいくつかの便利なボタンがあり、それらはファイルを開く、保存、全てを保存、等々です。「実行」のボタンは非常に重要です。普通は、これは右向き三角の「再生」ボタンのようなラベルになっています。これを押下すると、あなたのコードがコンパイルされ、なにも問題が発生しなければ自動的にそれを実行します。ですのでこれは頻繁に使われるボタンです。
- ファイルセレクタとプロジェクトナビゲータ領域：ここではプロジェクトとそれに関連するファイルを見ることができます。通常、これは階層付きの整列されたファイルのリストとして表示されます。ここではあなたのプロジェクトに固有のファイルに加えて、全ての oF のライブラリファイルを見ることができます。
- 編集エリア：プロジェクトナビゲーション領域からファイルを、通常はファイルをダブルクリックして開くと、それは編集領域で開くはずです。これはほとんど通常のテキストエディタのような見た目で、ほぼ同じように振る舞います。
- コンソール：ここにあなたのアプリが、実行中にメッセージを出力します。このメッセージはデバッグ時に本当に有用です。`cout` コマンドや[`ofLog(...)`](http://openframeworks.cc/documentation/utils/ofLog.html "ofLog ドキュメントページ") 関数を使ってテキストメッセージをコンソールに出力できます。

<!--
#### Apple Xcode
-->

#### Apple Xcode

<!--
[Xcode](https://developer.apple.com/xcode/ "Xcode website") is Apple's IDE. It is used both for iOS apps and desktop apps. Even though there are other IDEs for OS X, Xcode is a pretty mature one with lots of nice and useful features, especially for dealing with iOS apps.
-->

[Xcode](https://developer.apple.com/xcode/ "Xcode のウェブサイト") は Apple の IDE です。iOS とデスクトップのアプリにも利用されています OS X 向けには他の IDE もありますが、Xcode はとても成熟していて、特に iOS アプリを扱う場合には多くの素敵で便利な機能があります。

<!--
Use the latest version of Xcode and read the setup guide.
-->

最新のバージョンの Xcode を利用して設定ガイドを読んでください。

<!--
![Xcode screenshot](images/XcodeScreenShot.jpg "XCode screenshot")
-->

![Xcode screenshot](images/XcodeScreenShot.jpg "XCode のスクリーンショット")

<!--
#### Microsoft Visual Studio 2012 Express
-->

#### Microsoft Visual Studio 2012 Express

<!--
[Visual Studio](http://visualstudio.com/ "Visual Studio website") is Microsoft's IDE, which is aimed at Windows development. It's a commercial product, but there's a free version you can download called "Express".
-->

[Visual Studio](http://visualstudio.com/ "Visual Studio のウェブサイト") は Microsoft の IDE で、Windows の開発用です。これは商用のプロダクトですが、"Express"と言う無料のバージョンもあります。

<!--
![Visual Studio screenshot](images/VS_ScreenShot.jpg "Visual Studio screenshot")
-->

![Visual Studio screenshot](images/VS_ScreenShot.jpg "Visual Studio のスクリーンショット")

<!--
#### Code::Blocks
-->

#### Code::Blocks

<!--
[Code::Blocks](http://codeblocks.org/ "Code::Blocks website") is a free/libre IDE. It runs on several platforms, but oF supports it for Microsoft Windows and Linux. It is quite "light" in terms of downloading and we (the contributors to this book) use it in workshops over Visual Studio, which can be a bit intimidating for beginners. For Microsoft Windows, follow the setup instructions (including step "e") carefully. There are scripts that help install dependencies and the Code::Blocks IDE for Linux.
-->

[Code::Blocks](http://codeblocks.org/ "Code::Blocks のウェブサイト") は無料/自由な IDE です。これは複数のプラットフォーム上で動作しますが、oF は Microsoft Windows と Linux 向けのみサポートします。これはダウンロードの観点で非常に「軽量」で我々（このブックのコントリビュータ）は、ビギナーには少し自信を失わせるような Visual Studio よりもこれをよく利用しています。Microsoft Windows 向けには、（ステップ"e"を含む）設定ガイドに注意深く従ってください。Linux 向けには依存ファイルと Code::Blocks IDE のインストールを助けるスクリプトが存在します。

<!--
![Code::Blocks screenshot](images/oF_codeblocks_1.png "Visual Studio screenshot of empty project")
-->

![Code::Blocks のスクリーンショット](images/oF_codeblocks_1.png "Visual Studio の空のプロジェクトのスクリーンショット")

<!--
## Running examples
-->

## サンプルの実行

<!--
Find the oF version that you downloaded and decompress it. From now on we will refer to this folder as the oF root folder. You can place the oF root folder anywhere you like. One thing to stress is that oF is designed to be self-contained -- everything you need will stay in one folder and this folder can even be moved around on your drive if need be. If you download another version of openFrameworks, it should stay in its own folder and don't try to merge them.
-->

ダウンロードした oF バージョンを見つけ、展開してください。以降、このフォルダを oF のルートフォルダと呼びます。この oF ルートフォルダはお好きな場所に置くことができます。強調すべき点の一つは oF は自己充足的にデザインされていて、必要なものは全て一つのフォルダに置かれていて、このフォルダは必要に応じてあなたのハードドライブのどこにも移動できるということです。もし別のバージョンの openFrameworks をダウンロードしたとした場合、それは独自のフォルダに置き、統合しようとしないでください。

<!--
Open it. Inside of it, you will find several folders which we will describe below in more detail. For now, navigate to the examples folder and let's try to compile examples/graphics/graphicsExample. If you are on OS X, click on the graphicsExample.xcodeproj. If you are using Visual Studio, choose the ".sln" file. On Code::Blocks, choose the ".workspace" file.
-->

開いてみましょう。中にはいくつかのフォルダがあり、これらは以下でより詳しく説明します。今は、examples フォルダに行って exapmles/graphics/graphisExample をコンパイルしてみましょう。もし OS X であれば、graphicsExample.xcodeproj をクリックしてください。Visual Studio ならば".sln"ファイルを選択してください。Code::Block の場合は".workspace"ファイルを選びます。

<!--
_A quick side note about workspace files. The reason we ask you to open those rather than the project file is that they contain a sub-project to build the oF library also. If you have any doubts, please read the readme for your given platform._
-->

_ワークスペースファイルについての簡単な覚書。プロジェクトファイルでなくこれらを開くように言っているのは、これらが oF ライブラリをビルドするサブプロジェクトも含んでいるからです。もし疑問があれば、任意のあなたのプラットフォームの readme を読んでください。_

<!--
Now your IDE should open and load this example. It should look like the IDE screenshots above. Locate the "Run" button or menu option and click on it. The example should compile (which might take a while, since the first time you compile you are also compiling the oF library). You'll see a lot of files being compiled the first time -- don't worry, this will just happen once when the oF library needs to be rebuilt. Feel free to get a cup of coffee or stretch. Long compile times are great moments to take a screen break.
-->

IDE がこのサンプルを開き、読み込んだはずです。上にある IDE のスクリーンショットのように見えると思います。”Run"ボタンまたはメニューの項目を見つけてクリックします。サンプルがコンパイルされます（少し時間がかかるかもしれません、なぜならば初回のコンパイル時には oF ライブラリもコンパイルするからです）。初回はたくさんのファイルがコンパイルされていることに気づくでしょう。ご心配なく、これは oF ライブラリの再ビルドが必要な時にだけ発生します。ご自由にコーヒーを飲んだり、ストレッチでもしましょう。長いコンパイル時間は画面から目を離す素晴らしい時間です。

<!--
If everything went well, a new window will pop up and display the example you just compiled. If this happened, congrats! You just have installed and compiled openFrameworks successfully and you are ready to go on. If this didn't happen, the first rule is, don't panic! Check the notes below for each IDE and be sure to read the release notes that come with oF.
-->

全て順調なら、ウインドウがポップアップして、たった今コンパイルしたサンプルが表示されるでしょう。こうなったら、おめでとう！これで openFrameworks のインストールとコンパイルが正しく実行され、あなたは前に進むことができます。もしそうなっていなければ、最初のルールは、あわてずに！下にあるそれぞれの IDE 用の注釈を確認して、oF に同梱されるリリースノートを必ず読んでください。

<!--
- Xcode: make sure that the pop-down menu just at the right of the run button has selected the item with the name of your example and not the one named "openFrameworks." There might be more than one item with the name of the example you are trying to run. Select any one of them as long as it is not the one named "openFrameworks". This pop-down menu selects the target you want to compile. If "openFrameworks" is selected you will just compile the openFrameworks core and not the example code. When you select the other items Xcode will compile both the oF core and the code for your example and when done, run the example.
- Visual Studio: make sure you've opened the .sln file. Visual Studio Express doesn't have a triangle button by default (I think it looks like a gear for debugging). Locate the [run without debugging option](http://social.msdn.microsoft.com/Forums/vstudio/en-US/7b2182f9-0e46-4e6f-a8db-3ab5af39f14b/start-without-debugging-option-missing-from-debug-menu?forum=vsdebug), which you can add to the menu bar if you want to customize the IDE.
- Code::Blocks: make sure you've opened the .workspace file. If you are opening up other projects, be sure to close the current workspace first, as Code::Blocks doesn't handle multiple open projects very well.
- all IDEs: the play button will compile and run the project, but sometimes you might need to hit the button twice if the window doesn't launch.
-->

- Xcode：実行ボタンのすぐ右にあるポップダウンメニューがサンプル名を選択しており、"openFrameworks"という名前のものでないことを確認してください。実行しようとするサンプルの名前は一つだけではないかもしれません。"openFrameworks"という名前のものでなければ、そのうちどれでも選択して良いです。このポップダウンメニューはコンパイルするターゲットを選択しています。"openFramworks"が選択されていると、openFrameworks のコアだけがコンパイルされてサンプルコードはされません。それ以外を選択していれば Xcode は oF のコアとサンプルのコードをコンパイルし、完了すれば、サンプルを実行します。
- Visual Studio：.sln ファイルを開いていることを確認してください。Visual Studio Express はデフォルトでは三角形のボタンがありません（デバッグ用のギアのように見えます）。[run without debugging オプション](http://social.msdn.microsoft.com/Forums/vstudio/en-US/7b2182f9-0e46-4e6f-a8db-3ab5af39f14b/start-without-debugging-option-missing-from-debug-menu?forum=vsdebug)を見つけてください、IDE をカスタマイズしたければこれをメニューバーに追加することができます。
- Code::Blocks：.workspace ファイルを開いていることを確認してください。他のプロジェクトを開いている場合、Code::Block は複数のプロジェウトが開かれることをうまく処理できないので、まずはじめに現在の workspace を閉じてください。
- 全ての IDE：再生ボタンはプロジェクトをコンパイルして実行しますが、時たまウインドウが開かない場合はボタンを 2 回押す必要がある場合があります。

<!--
If the graphics example works, spend some time going through the other oF examples and running them. Usually, it's good practice to close the current project / workspace completely before you open another one. Once the oF library is compiled, the projects should build quite quickly!
-->

graphics サンプルが動作したら、少し時間を使って他の oF サンプルを見て回り、実行してみましょう。通常、別のプロジェクトを開く前に現在のプロジェクト/ワークスペースを完全に閉じることは良い習慣です。oF ライブラリが一度コンパイルされてしまえば、プロジェクトは非常に早くビルドされるはずです！

<!-- If you have trouble, please keep track of what errors you have, what platform you are on, and start using the [oF forum](http://forum.openframeworks.cc/) to find help. There are years of experience there, and really helpful folks who can help answer questions. First, try searching for a specific error and if you don't see it, post a question on the forum. When you are beginning it can be quite frustrating, but the community is very good at helping each other out.
-->

問題があれば、どんなエラーが起きたか、なんのプラットフォーム上かを調べて [oF フォーラム](http://forum.openframeworks.cc/)、[oF フォーラム](http://forum.openframeworks.cc/) でヘルプを探してみてください。そこには何年もの経験が蓄積され、質問に答えてくれるとても頼りになる仲間がいます。はじめは特定のエラーについて検索してみて、もし見つからなければフォーラムに質問を投稿しましょう。最初はとてもイライラするかもしれませんが、このコミュニティはお互いにとてもよく助け合っています。

<!--
Once done continue reading.
-->

終わったら読み続けましょう。

<!--
## oF folder structure
-->

## oF のフォルダ構造

<!--
Inside the oF root folder you will find several other folders, at least, the following:
-->

oF ルートフォルダの中にはいくつかのフォルダがあり、少なくとも以下のものがあります。

<!--
### Addons
-->

### Addons

<!--
The "addons" folder will contain the included "core" addons. Addons are extra pieces of code that extend oF's functionalities, allowing you to do almost anything with oF. Addons are usually written by third parties that have shared these. The "core" addons, the ones already included in your oF download, are addons that are used so frequently that it has been decided to include them as part of the official oF download. These are coded and maintained by oF's core developers.
Check the examples/addons folder in your oF root folder where you will find at least one example of how to use each of these addons.
You can also go to [ofxAddons](http://ofxaddons.com/ "ofxaddons, a collection of oF addons") where you'll find a huge collection of additional addons from the community.
-->

"addons" フォルダには同梱されている「コア」のアドオンが入っています。アドオンは oF の機能を拡張するための追加のコード片で、oF でほとんどどんな事でも可能にしてくれます。アドオンは通常はこれを共有してくれたサードパーティによって書かれています。「コア」アドオンは oF のダウンロードにすでに含まれていますが、これはとても頻繁に利用されるので公式の oF ダウンロードの一部として含めるようにされたものです。これらは oF のコアデベロッパによりプログラミングおよびメンテナンスされています。
oF ルートフォルダの examples/addons フォルダには、少なくとも一つはそれぞれのアドオンの使い方のサンプルがあります。
または[ofxAddons](http://ofxaddons.com/ "ofxaddons、 oFアドオンコレクション")では、コミュニティからの追加のアドオンの膨大なコレクションを見ることができるでしょう。

<!--
### Apps
-->

### Apps

<!--
This is the folder where you put your project files as you make new projects. Your current oF download contains the folder named "myApps" inside of "apps", and this is where the project generator will default to when you make a new project. One important thing to note is that the project is positioned relatively to the libs folder, i.e. if you were to look inside the project file you'd see relative folder paths, i.e. `../../../libs`. This image is showing how `../../../libs` might work visually:
-->

これはあなたが新規プロジェクトを作成した際にプロジェクトのファイルが置かれるフォルダです。現在の oF ダウンロードファイルには "apps" 野中に "myApps" という名前のフォルダが含まれていて、これは新規プロジェクトを作る時にプロジェクトジェネレータがデフォルトとしている場所です。注記すべき大事な点はプロジェクトは libs への相対的な位置に置かれているということです、例えばプロジェクトファイルの中を見たとして、例えば`../../../libs`というような相対のフォルダパスがあるでしょう。この画像は`../../../libs`がどのように動作するかを視覚的に示しています。

<!--
![app position to root](images/projectPlacement.png)
-->

![app のrootに対する位置](images/projectPlacement.png)

<!--
A key thing to note is that your project files always have to live at this depth from the root. If you alter their depth, they won't find the other pieces they need to compile. This is a very common mistake for beginners, especially as you start to find example projects and bring them in oF to test, etc. Please make sure you understand that projects are always setup relative to the root level. This is what makes the whole oF folder able to be anywhere on your hard drive -- it's a self-contained package. This is probably the #1 issue beginners have, so it's worth emphasizing.
-->

重要な点は、プロジェクトファイルは常にルートからこの深さの階層になければいけないということです。深さを変えてしまうと、それらはコンパイルに必要な他の要素を見つけられなくなってしまいます。これは、特にサンプルプロジェクトを見つけて oF の中にテストのために移動することなど、ビギナーにとてもよくある失敗です。プロジェクトは常にルート階層からの相対でセットアップされることをきちんと理解してください。このこと、自己充足的なパッケージであることが oF フォルダ全体がハードディスクのどこにでも置くことを可能にしているのです。これはおそらくビギナーが経験する一番の問題ですので、強調する価値があります。

<!--
### Examples
-->

### Examples

<!--
This is a folder with examples, sorted by topic. There are a big bunch of examples that cover almost all of aspects oF. Each example is made with the idea of keeping it simple and focused on the particular aspect it tries to address. Therefore it should be easily understandable and a good starting point when you want to do something similar in your project.
-->

これはサンプルの入っているフォルダで、トピック別に並んでいます。oF のあらゆる側面をカバーするたくさんのサンプルが入っています。それぞれのサンプルはシンプルでありながら取り組んでいる特定の側面にフォーカスするという考えで作られています。したがって容易に理解可能でありながら、あなたのプロジェクトにおいて似た何かを行いたい場合の良いスタート地点になるでしょう。

<!--
### libs
-->

### libs

<!--
These are the libraries that openFrameworks uses to compile your project. They include things like [FreeType](http://freetype.org/ "FreeType website") for typography support, [FreeImage](http://freeimage.sourceforge.net/ "FreeImage project website") for image loading, glfw for windowing, etc. Also, the code for openFrameworks is in libs, as well as the project files that help compile oF. If you need to look at the source code, here's where to look.
-->

これらは openFrameworks がプロジェクトをコンパイルするために利用するライブラリです。タイポグラフィのサポートのための[FreeType](http://freetype.org/ "FreeType のウェブサイト")や、画像読み込みのための[FreeImage](http://freeimage.sourceforge.net/ "FreeImage プロジェクトのウェブサイト")、ウインドウのための glfw 等を含みます。加えて、 openFrameworks のコードも、それをコンパイルするためのプロジェクトファイルと共に libs の中にあります。ソースコードを見る場合はここを見てください。

<!--
### other
-->

### other

<!--
Here you'll find an [Arduino](http://www.arduino.cc/ "website if the Arduino single-board microcontroller") sketch for using the serial example located at examples/communication/. This is handy to check that your serial communication with Arduino is set up correctly and working.
-->

ここには examples/communication/ にあるシリアル通信のサンプルを使うための[Arduino](http://www.arduino.cc/ "website if the Arduino single-board microcontroller")のスケッチがあります。これで Arduino とのシリアル通信が正しく設定されて動作しているかを簡単にチェックできます。

<!--
### projectGenerator
-->

### projectGenerator

<!--
oF now ships with a simple project generator which is really useful for making new projects. One of the larger challenges has always been making a new project. This tool takes a template (located in the scripts folder) and modifies it, changing the name to a new one that you choose and even allowing you to specify addons. It allows you to place the project anywhere you want, and while we've structured all the examples to be a certain distance away from the root, you can set the position using this tool (e.g. if you put the project deeper, it will change the `../../../libs` to `../../../../libs`). It's designed to make it easy / trivial to start sketching in code, without worrying too much about making a new project. In the past, we've always recommended that you copy an old project and rename it, but this is a more civilized approach to making projects. Check the readme file where the usage of this app is described.
-->

現在の oF はシンプルなプロジェクト生成ツールを備えており、これは新規プロジェクトを作成するためにとても便利です。いつでも最大のチャレンジの一つは新規のプロジェクトの作成です。このツールは（scripts フォルダにある）テンプレートを利用してそれを改変し、名前をあなたが選択した新しいものに変更し、アドオンも選択できます。プロジェクトは望む場所どこにでも配置することができ、全てのサンプルはルートから任意の場所にあるように構成されていますが、このツールでその位置を設定することができます（例　プロジェクトをより深い階層に置けば、`../../../libs`は`../../../../libs`に変更されます）。これは新規プロジェクトを作成することに対して心配せずに、コードをスケッチをすることを簡単かつ平凡なことにしてくれます。過去には、我々は常に古いプロジェクトをコピーしてリネームすることを推奨してきましたが、こちらがプロジェクト作成のより快適なやりかたです。このアプリの利用方法が記述されている readme ファイルを見てみてください。

<!--
## The oF Pantry
-->

## The oF Pantry

<!--
Your default new kitchen will only have tools for coding, but the oF kitchen comes with a super nice pantry, filled up with really nice, cool and useful stuff.
-->

デフォルトの新しいキッチンはコーディングのための道具だけがありますが、oF のキッチンにはとても素敵なパントリーがあり、本当に素敵でクールなものが詰まっています。

<!--
Imagine that you want to cook something but your kitchen has no pantry or if there is one it is completely empty. Cooking anything would be quite difficult under such conditions, as you'd have to go out and buy the things you need and you probably won't find everything in one outing. This is not a nice scenario, especially if you want to get creative and make awesome things.
-->

何かを調理したいとして、キッチンにパントリーが存在しないか、まったく空のものが一つだけあることを想像してください。そのような状況下では何を作るのも非常に困難で、必要なものは外に買いに出かける必要がありますし、一度の外出ではきっと必要な全ては見つからないでしょう。これは、特にクリエイティブになって驚くべき物を作るときに良いシナリオではありません。

<!--
So, what happens when you have your pantry filled with oF's components? You will be able to cook whatever you want because some really good ingredients are already there. Additionally, there are some really nice tools in there. This will let you complete recipes in a short amount of time, leaving you more time to get creative and try out new and more delicious recipes.
-->

それでは、oF コンポーネントが詰まったパントリーがあったとしたら何が起きるでしょうか？あなたは望むものをなんでも調理できるでしょう、なぜなら非常に良い食材がそこにすでにあるからです。加えて、とても良い道具もあります。これはレシピを短い時間で完成させ、よりクリエイティブになって新しくより美味しいレシピに挑戦するための時間を残してくれます。

<!--
### What is inside the oF pantry
-->

### パントリーには何があるのか

<!--
Here you will find a lot of different things, from ingredients to tools, all ordered according to use. This is a breakdown of how oF code is organized (as well as the examples) and should give you a sense of what oF contains:
-->

ここにはたくさんの色々なものがあり、素材から道具まで使い道によって整頓されています。これは oF のコードがどのように管理されているかの分類（サンプルも含め）であり、oF が何を含んでいるかの感じが分かるでしょう。

<!--
- **3D**
  - tools for drawing basic 3D polygonal objects, such as spheres, cubes, pyramids, etc.
  - [`ofCamera`](http://openframeworks.cc/documentation/3d/ofCamera.html "ofCamera Documentation Page"), [`ofEasyCam`](http://openframeworks.cc/documentation/3d/ofEasyCam.html "ofEasyCam Documentation Page"), 3D cameras for navigating and viewing your 3D scene, either interactively or not
  - [`ofNode`](http://openframeworks.cc/documentation/3d/ofNode.html "ofNode Documentation Page"), a 3D point in space, which is the base type for any 3D object, allowing it to be moved, rotated, scaled, nested and drawn
  - [`ofMesh`](http://openframeworks.cc/documentation/3d/ofMesh.html "ofMesh Documentation Page"), a primitive for batching points in 3D space that allows you to draw them in several different ways such as points, lines, line strips, triangles, triangle strips, and attach textures (images) to these. All of this is done very efficiently using your computer's GPU
  - functions to help load and save 3D objects
-->

- **3D**
  - 基本的な 3D ポリゴンのオブジェクトを描画するツール、例えば球体、立方体、角錐等。
  - [`ofCamera`](http://openframeworks.cc/documentation/3d/ofCamera.html "ofCamera ドキュメントページ")、[`ofEasyCam`](http://openframeworks.cc/documentation/3d/ofEasyCam.html "ofEasyCam ドキュメントページ")、インタラクティブか否かを問わず 3D シーンをナビゲートして見るための 3D カメラ。
  - [`ofNode`](http://openframeworks.cc/documentation/3d/ofNode.html "ofNode ドキュメントページ")、空間における 3D の点、あらゆる 3D オブジェクトの基礎で、それらを移動、回転、拡縮、ネスト化および描画させる。
  - [`ofMesh`](http://openframeworks.cc/documentation/3d/ofMesh.html "ofMesh ドキュメントページ")、3D 空間での点をまとめるプリミティブで、それらを点、線分、線、トライアングル、トライアングル片といった様々な方法で描画し、テクスチャ（画像）を適用させる。これらの全てはコンピュータの GPU を利用して非常に効率的に行われる。
  - 3D オブジェクトの読み込みと保存のための関数

<!--
- **app**
  - tools for setting and getting properties of your app such as window size, position, different drawing modes, frame rate, etc.
  - different windowing systems, such as [`ofAppNoWindow`](http://openframeworks.cc/documentation/application/ofAppNoWindow.html "ofAppNoWindow Documentation Page") which sets up openFrameworks in a windowless context
-->

- **アプリ（apps）**
  - ウインドウサイズ、位置、異なる描画モード、フレームレートといったアプリのプロパティの設定と取得のツール
  - openFrameworks をウインドウレスなコンテキストでセットアップする [`ofAppNoWindow`](http://openframeworks.cc/documentation/application/ofAppNoWindow.html "ofAppNoWindow ドキュメントページ") などの様々なウインドウシステム

<!--
- **communication**
  - [`ofSerial`](http://openframeworks.cc/documentation/communication/ofSerial.html "ofSerial Documentation Page") provides simple serial port communication
  - [`ofArduino`](http://openframeworks.cc/documentation/communication/ofArduino.html "ofArduino Documentation Page") allows openFrameworks to communicate via [Firmata](http://playground.arduino.cc/Interfacing/Firmata "Arduino reference for Firmata")
  -->

- **通信（communication）**
  - [`ofSerial`](http://openframeworks.cc/documentation/communication/ofSerial.html "ofSerial ドキュメントページ")はシンプルなシリアルポート通信を提供します。
  - [`ofArduino`](http://openframeworks.cc/documentation/communication/ofArduino.html "ofArduino ドキュメントページ")は openFrameworks の [Firmata](http://playground.arduino.cc/Interfacing/Firmata "Arduino の Firmata リファレンス") 経由での通信を可能にします。

<!--
- **events**
  - the oF event manager, allowing you to tap into app events if you need or even creating your own events
-->

- **イベント（events）**

  - 必要なときにイベントを送ったり、または独自のイベントを作成もできる oF イベントマネージャ

<!--
- **gl**
  - [OpenGL](https://en.wikipedia.org/wiki/OpenGL "Wikipedia article on OpenGL"), the library for using the computer's [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit "Wikipedia article on the graphics processing unit")
  - contains GL specific functionality such as VBOs (Vertex Buffer Object), FBOs (Frame Buffer Object), Renderers, Lights, Materials, Shaders, Textures, and several other GL utilities
  - oF implements different rendering pipelines (fixed, programmable & OpenGL ES (used on less powerful devices such as smartphones and the Raspberry Pi)) -- most of this code is found in the gl folder
-->

- **gl**
  - コンピュータの [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit "GPU の Wikipedia 記事") を利用するためのライブラリである [OpenGL](https://en.wikipedia.org/wiki/OpenGL "OpenGL の Wikipedia 記事")
  - VBO (頂点バッファオブジェクト)、 FBO (フレームバッファオブジェクト)、 レンダラ、 ライト、 マテリアル、 シェーダ、 テクスチャといった GL 固有の機能、およびその他の GL ユーティリを含みます。
  - oF は様々なレンダリングパイプラインを実装しています （固定、 プログラマブル & OpenGL ES （スマートフォンや Raspberry Pi といった非力なデバイスで利用されます）） -- このコードの大部分は gl フォルダにあります

<!--
- **graphics**
  - capabilities such as loading, drawing and saving images of almost any kind, e.g. via [`ofImage`](http://openframeworks.cc/documentation/graphics/ofImage.html "ofImage Documentation Page")
  - also allows you to render as PDF
  - several different methods for drawing in 2D, and exhibiting colors and styles
  - most of the drawing tools rely on OpenGL so these are usually very fast
  - typography with several kinds of rendering options and utilities e.g. [`ofTrueTypeFont`](http://openframeworks.cc/documentation/graphics/ofTrueTypeFont.html "ofTrueTypeFont Documentation Page"), a library for loading and drawing [TrueType fonts](https://en.wikipedia.org/wiki/TrueType "Wikipedia article on TrueType font format")
-->

- **グラフィックス（graphics）**
  - [`ofImage`](http://openframeworks.cc/documentation/graphics/ofImage.html "ofImage ドキュメントページ") を通じた
    ほとんどあらゆる種類の画像の読み込み、描画、保存機能
  - PDF としての描画も可能
  - 2D での描画、カラーやスタイルの表示のための様々な手法
  - 大部分の描画ツールは OpenGL に依存しているのでこれらは通常非常に高速
  - 何種類かのレンダリングオプションやユーティリティを備えたタイポグラフィ。例えば　[TrueType fonts](https://en.wikipedia.org/wiki/TrueType "TrueType フォント形式 の Wikipedia 記事") の読み込みおよび描画ライブラリである [`ofTrueTypeFont`](http://openframeworks.cc/documentation/graphics/ofTrueTypeFont.html "ofTrueTypeFont ドキュメントページ")

<!--
- **math**
  - mostly math related tools
  - vectors (i.e. [`ofVec2f`](http://openframeworks.cc/documentation/math/ofVec2f.html "ofVec2f Documenation Page"), [`ofVec3f`](http://openframeworks.cc/documentation/math/ofVec3f.html "ofVec3f Documentation Page"))
  - matrices (i.e. [`ofMatrix3x3`](http://openframeworks.cc/documentation/math/ofMatrix3x3.html "ofMatrix3x3 Documenation Page"), [`ofMatrix4x4`](http://openframeworks.cc/documentation/math/ofMatrix4x4.html "ofMatrix4x4 Documenation Page"))
  - quaternions (i.e. [`ofQuaternion`](http://openframeworks.cc/documentation/math/ofQuaternion.html "ofQuaternion Documentation Page"))
  - useful math help functions like [`ofRandom`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofRandom "ofRandom Documentation Page") and [`ofNoise`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofNoise "ofNoise Documentation Page").
-->

- **数学（math）**
  - ほとんどの数学関連のツール
  - ベクタ (例 [`ofVec2f`](http://openframeworks.cc/documentation/math/ofVec2f.html "ofVec2f ドキュメントページ")、 [`ofVec3f`](http://openframeworks.cc/documentation/math/ofVec3f.html "ofVec3f ドキュメントページ"))
  - 行列 (例 [`ofMatrix3x3`]（http://openframeworks.cc/documentation/math/ofMatrix3x3.html "ofMatrix3x3 ドキュメントページ"）、 [`ofMatrix4x4`]（http://openframeworks.cc/documentation/math/ofMatrix4x4.html "ofMatrix4x4 ドキュメントページ")
  - クォータニオン(例 [`ofQuaternion`]（http://openframeworks.cc/documentation/math/ofQuaternion.html "ofQuaternion ドキュメントページ")
  - [`ofRandom`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofRandom "ofRandom ドキュメントページ") や [`ofNoise`](http://openframeworks.cc/documentation/math/ofMath.html#!show_ofNoise "ofNoise ドキュメントページ") といった便利な数学のヘルプ関数

<!--
- **sound**
  - low level sound access directly on sound card, e.g. [`ofSoundStream`](http://openframeworks.cc/documentation/sound/ofSoundStream.html "ofSoundStream Documentation Page")
  - higher level code for playing samples and sound effects, e.g. [`ofSoundPlayer`](http://openframeworks.cc/documentation/sound/ofSoundPlayer.html "ofSoundPlayer Documentation Page")
-->

- **サウンド（sound）**
  - 低レベルなサウンドカードへの直接アクセス。例 [`ofSoundStream`](http://openframeworks.cc/documentation/sound/ofSoundStream.html "ofSoundStream ドキュメントページ")
  - サンプリングや SE の再生の高レベルのコード。例 [`ofSoundPlayer`](http://openframeworks.cc/documentation/sound/ofSoundPlayer.html "ofSoundPlayer ドキュメントページ")

<!--
- **base types**
  - a lot of different base types for common elements used extensively within oF
  - mostly for folks that want to understand the architecture of oF,
-->

- **ベースタイプ（base types）**
  - oF 内で広範囲に使われる共通要素のための様々なベースタイプ（基本型）
  - ほとんど、oF のアーキテクチャを理解したい人向け

<!--
- **utils**
  - utilities for
    - file input and output (also via URLs)
    - logging
    - threading
    - system dialogs (open, save, alert)
    - reading and saving [XML](https://en.wikipedia.org/wiki/XML "Wikipedia article on XML") files (super useful for storing and reading your app's settings)
  - e.g. [`ofDirectory`](http://openframeworks.cc/documentation/utils/ofDirectory.html "ofDirectory Documentation Page") can help iterate through a directory
-->

- **ユーティリティ（utils）**
  - 下記のユーティリティ
    - ファイル入出力（URL 経由も含む）
    - ロギング
    - スレッド
    - システムダイアログ（開く、保存、アラート）
    - [XML](https://en.wikipedia.org/wiki/XML "XML のWikipedia記事") ファイルの読み込みと保存（アプリの設定の保存と読み出しに非常に有用）
  - 例 [`ofDirectory`]（http://openframeworks.cc/documentation/utils/ofDirectory.html "ofDirectory ドキュメントページ"）がディレクトリを走査する助けになります

<!--
- **video**
  - video grabber and player, with behind-the-scenes implementations for all the supported platforms.
  - [`ofVideoGrabber`](http://openframeworks.cc/documentation/video/ofVideoGrabber.html "ofVideoGrabber Documentation Page") helps with grabbing from a webcam or attached camera
  - [`ofVideoPlayer`](http://openframeworks.cc/documentation/video/ofVideoPlayer.html "ofVideoPlayer Documentation Page") helps with playing video files
-->

- **ビデオ（video）**
  - サポートされる全てのプラットフォーム向けに背後で実装されている動画のキャプチャと再生
  - [`ofVideoGrabber`](http://openframeworks.cc/documentation/video/ofVideoGrabber.html "ofVideoGrabber ドキュメントページ")によるウェブカムや接続されたカメラからのキャプチャ
  - [`ofVideoPlayer`](http://openframeworks.cc/documentation/video/ofVideoPlayer.html "ofVideoPlayer ドキュメントページ") による動画ファイルの再生

<!--
### Addons
-->

### アドオン

<!--
As mentioned before, addons extend oF core functionalities. In each oF distribution there are several included addons, usually referred to as "core addons":
-->

既述の通り、アドオンは oF のコア機能を拡張します。各々の oF ディストリビューションにはそれぞれアドオンがいくつか同梱されており、「コアアドオン」と呼ばれます。

<!--
- **ofx3DModelLoader**
  Used for loading 3D models into your oF project. It only works with .3ds files.
- **ofxAssimpModelLoader**
  Also loads 3D models into your oF project, but it is done using the [assimp](http://assimp.sourceforge.net/) library, which supports a wide variety of 3D file formats, even animated 3D objects.
- **ofxGui**
  This is the default GUI (Graphical User Interface) for oF. It lets you add sliders and buttons so you can easily modify parameters while your project is running. It relies heavily on ofParameters and ofParameterGroup. It allows you to save and load the values for the parameters that you've adjusted.
- **ofxKinect**
  As you probably infer, it's for using a [Microsoft XBox Kinect](https://en.wikipedia.org/wiki/Kinect) 3D sensor with your oF project. This addon relies on [libfreenect](http://openkinect.org/wiki/Main_Page), so you can only access the depth and RGB images that the Kinect reads and adjust some of its parameters, like tilt and light. It includes some handy functions that allow you to convert Kinect's data between several different kinds. Please note that ofxKinect doesn't perform skeleton tracking. For such thing you need to use ofxOpenNI.
- **ofxNetwork**
  Lets you deal with network protocols such as UDP and TCP. You can use it to communicate with other computers over the network. Check out the network chapter for more information.
- **ofxOpenCv**
  This is oF's binding to one of the best and most used computer vision code library, [OpenCV](http://opencv.org/). Computer vision is a complete world in itself, and being able to use OpenCV right out-of-the-box is a super important and useful oF feature.
- **ofxOsc**
  OSC (Open Sound Control) implementation for oF. OSC easily communicates with other devices or applications within the same network. OSC is used to send messages and parameters from one app to another one. Several chapters in this book discuss OSC.
- **ofxSvg**
  Loads and displays [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "Wikipedia article on SVG") files. These are vector graphics files, usually exported from vector drawing programs such as Inkscape or Adobe Illustrator.
- **ofxThreadedImageLoader**
  Loads images on a different thread, so your main thread (the one that draws to your screen) doesn't get stuck while loading images. Really useful when loading online images.
- **ofxVectorGraphics**
  Used to write out [EPS](https://en.wikipedia.org/wiki/Encapsulated_PostScript "Wikipedia article on encapsulated PostScript (eps)") vector graphics files. It the same drawing syntax as oF's regular drawing syntax, so it is really easy to use. Check chapter **[add correct chapter number]** for more info about oF's drawing capabilities.
- **ofxXmlSettings**
  This is oF's simple XML implementation used mostly for loading and saving settings.
-->

- **ofx3DModelLoader**
  3D モデルを oF プロジェクトに読み込むために利用します。これは .3ds ファイルにのみ使えます。
- **ofxAssimpModelLoader**
  同様に 3D モデルを oF プロジェクトに読み込みますが、[assimp](http://assimp.sourceforge.net/)ライブラリを利用していて、幅広い 3D ファイルフォーマット、動きのある 3D オブジェクトもサポートします。
- **ofxGui**
  oF のデフォルトの GUI（グラフィカル・ユーザー・インターフェース）です。スライダーやボタンを利用でき、プロジェクトが動作している最中に容易にパラメタを調整することができます。これは oFParameters と ofParameterGroup に強く依存しています。調整したパラメタの保存や読み込みも可能です。
- **ofxKinect**
  ご推察の通り、これは[Microsoft XBox Kinect](https://en.wikipedia.org/wiki/Kinect)3D センサーを oF プロジェクトで利用するためのものです。このアドオンは[libfreenect](http://openkinect.org/wiki/Main_Page)に依存しているので、Kinect が読み取って傾きや明るさなどのパラメタを調整した深度および RGB イメージにのみアクセスができます。これは Kinect のデータを色々な種類に変換できる便利な関数も含んでいます。ofxKinect は骨格トラッキングは行わないことに注意してください。これには ofxOpenNI が必要です。
- **ofxNetwork**
  UDP や TCP といったネットワークプロトコルを扱います。ネットワーク越しに他のコンピュータと通信するために利用できます。詳しい情報はネットワークの章を参照してください。
- **ofxOpenCv**
  これは最高で最も利用されているコンピュータビジョンのライブラリである[OpenCV](http://opencv.org/)の oF バインディングです。コンピュータビジョンはそれ自体が完結した世界で、OpenCV をすぐに利用できることは非常に重要かつ oF のとても便利な機能です。
- **ofxOsc**
  OSC (Open Sound Control) の oF 実装です。OSC は同じネットワーク上のデバイスやアプリケーションと容易に通信が可能です。OSC はメッセージやパラメタをあるアプリから他に送る時に利用します。このブックのいくつかの章で OSC に触れています。
- **ofxSvg**
  [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "SVG のWikipedia記事") ファイルの読み込みと表示。これはベクタ形式のグラフィックファイルで、Inkscape や Adobe Illustator といったベクタ描画プログラムから出力されます。
- **ofxThreadedImageLoader**
  別スレッドから画像を読み込むので、メインスレッド（画面に描画を行うもの）は画像の読み込み中に停止しません。オンラインの画像を読み込む時にとても便利です。
- **ofxVectorGraphics**
  [EPS](https://en.wikipedia.org/wiki/Encapsulated_PostScript "encapsulated PostScript (eps) の Wikipedia 記事")ベクタグラフィックスファイル形式の出力。oF の通常の描画構文と同じなので、非常に使いやすいです。oF の描画機能については **[add correct chapter number]** を参照してください。
- **ofxXmlSettings**
  oF のシンプルな XML 実装で、設定の読み込みや保存によく使われます。

<!--
That's what's in the pantry. What do you want to cook?
-->

これらがパントリーにはあります。何を作りましょう？

<!--
![pantry, image courtesy [http://resultsroom.co.nz/stock-pantry-fridge/](http://resultsroom.co.nz/stock-pantry-fridge/)](images/pantry.jpg)
-->

![パントリー、画像提供 [http://resultsroom.co.nz/stock-pantry-fridge/](http://resultsroom.co.nz/stock-pantry-fridge/)](images/pantry.jpg)
