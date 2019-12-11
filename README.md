# いろいろなトッププレートの作り方

キーボードの打鍵感、見た目の大きな要素であるトッププレート。  
自作キーボード設計というと回路設計をしないといけないのかなーなんて思う方が多いのですが、
回路設計は手段であり、目的は快適にコンピュータと意思疎通を図ることです。

手前味噌ではありますが、回路設計できなくても無限の可能性があればオリジナルキーボードが作れるので、
トッププレートさえ設計できればあなたのオリジナルキーボードは完成したもも同然です。(暴走)  

今回は回路設計できない人向けトッププレート(≒オリジナルキーボード)の作り方を伝授しちゃいます。  
既にキーボード設計している人でも今まで作ったことのない素材でトッププレートを作ってみるきっかけになれば幸いです。

トッププレート加工方法と素材について
* PCB
  * Fr-4(ガラスエポキシ)
  * アルミ
* レーザー加工
  * アクリル
  * MDF
  * 金属
* 3Dモデリング
  * 樹脂フィラメント
  * アルミ削り出し
  * 鋳造、その他諸々


## PCBプレート

早速ではございますが、ここで一つ断っておきます。  
回路設計の必要はありませんが、Kicadはめちゃくちゃ使います！  
Inkscapeで設計してたときもあるのですが、mmとinchが入り乱れるキーボード設計では、Kicadのグリッドが一番ラクでした…  
そんな都合でまずいちばん手間が少ないPCBプレートの作り方を伝授します。

### 手順

1. Kicadをインストールして「01.pcb/sample.kicad_pcb」を開いてください。
2. スイッチやネジ穴、外形を好きな感じに並び替えて、足りなければコピペしてください。

完了です。笑

![](images/01.pcb/00.png)

「alt+3」で3Dビューアが起動します

![](images/01.pcb/01.png)

ベタとかシルクとかマスクとかはお好みで。(^^)b  
ネジ穴はEdge.cutsでもいいですが、スルーホールにするとメッキされてちょっとキレイです。

じつは基板データが公開されている既存のキーボードでも、
スイッチのフットプリントを↑に置き換えればトッププレートになります。

あとは製造会社のご指定の方法でガーバーってのをプロットしてお金払って到着を待ちます。

ボトムプレートはスイッチのフットプリントを消して再プロットです。  
無限の可能性でプロマイクロのおうちを使う場合、このフットプリントをボトムプレートに使うといいです。

発注先はElecrowさん、JLCPCBさん、ALLPCBさんなどがあります。


## レーザー加工データ

レーザー加工データはInkscapeで作りますが、まずネジ穴を外形(Edge.cutsレイヤー)に移すため、半径1.1mmの円に置き換えます(置き換えたのが「02.svg/sample/sample.kicad_pcb」)  
Kicadで「ファイル->エクスポート->SVG」でEdge.cutsレイヤーをエクスポートして、Inkscapeに読み込んでください。  
キャンパスのサイズ、線の太さや色などを業者さん指定の方法に従って変更し完了です。
簡単ですね。

![](images/02.svg/00.png)

彫刻などはお好みで。

発注先はElecrowさん、Emerge+さん、遊舎工房さんなどがあります。


## 3Dモデリング

モデリングソフトは界隈だとFusion360も多い印象ですが、
OS宗教上の理由でBlenderを使います。  
(Fusion360がLinuxで使えるようになってほしい)

まずはBlenderの簡単な操作方法を。


### Blender雑チートシート

まずはblenderの簡単な操作方法をまとめます。

* モード切替: Tab
  * オブジェクトモード: オブジェクトの選択、オブジェクト全体に対する操作
  * 編集モード: 選択したオブジェクトの各頂点、辺、面を操作

* 視点切替
  * 7: 上から
  * 1: 左から
  * 3: 前から
  * Ctrl+7: 下から
  * Ctrl+1: 右から
  * Ctrl+3: 後から
  * 5: 遠近法切替

* 選択系:
  * 右クリック: 選択
  * Ctrl+tab: 選択モード切替(頂点、辺、面)
  * a: 全選択/選択解除
  * c: 範囲選択
  * l: 隣接選択
  * Alt+右クリック: ループ選択(直接つながっている)
  * Ctrl+Alt+右クリック: リング選択(平行を選択)

* 編集系:
  * g: 移動
  * f: 面張り
  * e: 押出
  * s: 拡大縮小
  * r: 回転
  * del: 削除・融解
  * k: ナイフ
  * b: ベゼル(角丸)

* 表示系:
  * h: 選択物を非表示
  * alt+h: すべて表示
  * z: スケルトン切替
  * t: 左側のやつ(ツールシェルフ)
  * n: 右側のやつ

* その他:
  * alt+c: カーブ(SVG読んだあと)をメッシュに変更
  * ctrl+j: 複数オブジェクトを結合
  * ctrl+p: 別オブジェクトを分割

書いてて思ったけど、これ専用のキーボードほしいな。そのうち作ろ。


### ブーリアントラブルシュート

メッシュ同士の結合(AND)、差分(OR)などをしてくれるとっても便利なブーリアンモデファイ。  
とっても便利だけどとっても癖っぽい。  
キーボードにおいてはプレートからスイッチをくり抜いたり、ネジ穴を開けたりするのに使う。  
原因はたいてい法線の向きが揃っていないか、頂点や辺や面が接していることが原因。

法線というのは雑に言うと面の裏表。  
人間目線で明らかでもBlenderからみて裏表がどっちかわからなくなるとくり抜いたりくっつけたりできない。

↓はうまくいかない

↓こうするとうまくいく


### 手順

1. ファイルメニューからKicadからエクスポートしたSVGをインポートします。  
  ![](images/03.3D/01.png)
2. 縮小されて取り込まれているので、10000倍に拡大(s→10000)します。  
  ![](images/03.3D/02.png)
3. すべて選択してメッシュに変更(alt+c)し、結合(ctrl+j)します。  
  ![](images/03.3D/03.png)
4. まず編集モードに切替(tab)複数の面で構成されているネジ穴を一つの面にまとめます(f)。  
  ![](images/03.3D/04-1.png)
  ![](images/03.3D/04-2.png)
5. スイッチ、ネジ穴をそれぞれループ選択(alt+右クリック)し、別オブジェクトに分割(p)します。適当な名前つけとくといいです。  
  ![](images/03.3D/05.png)
6. 円弧は既に面張りされているので、面選択モード(ctrl+tab)で全選択(a)して、面張りし(f)、面のみ削除(del)し、残った斜辺を削除(del)ます。  
  ![](images/03.3D/06.png)
7. 頂点選択モード(ctrl+tab)で全選択して面張り(f)します。形状的に面が交差してしまう場合は複数回に分けて面張りし、最後に面を融解(del)するといいです。  
  ![](images/03.3D/07.png)
8. 作成した面を5mm押し出します(e→5)  
  ![](images/03.3D/08.png)
9. さきほど別オブジェクトに分割したスイッチ外形の編集モードに入り、最終的にブーリアンでくり抜くため、すべての頂点をz軸方向に-1mm移動(g→z→-1)し、各スイッチで面張りし、法線方向を*下*に揃え、7mm押し出します(e→7)  
  もし余裕があれば各スイッチで爪用の溝を0.5mmくらい作っておくと保持性が高まっていいです。
  ![](images/03.3D/09.png)
10. ネジ外形の編集モードに入り、すべての頂点をZ軸方向に6mm移動(g→z→6)し、法線方向を*上*に揃え、3mm押し出します(e→-3)  
11. ピポットポイントをそれぞれの原点にして、0mmで押出し(e→enter)、1.8倍(スペーサーが入る太さ)に拡大(s→1.8)し、更に4mm押出し(e→4)ます。  
  ![](images/03.3D/11.png)
12. せっかく3Dなので、上部の辺をループ選択して、丸みをつけ(ctrl+b)ます。(ツールシェルフ(t)で微調整可)  
  ![](images/03.3D/12.png)
13. メインのプレートのブーリアンモデファイでネジとスイッチをくり抜き、適用し、利用したスイッチ外形とネジ外形のオブジェクトを削除(del)します。  
  ![](images/03.3D/13.png)
14. ファイルメニューからSTLにエクスポートしておしまい。

他に比べると面倒に感じるかもしれませんが、慣れれば爪の溝を作っても1時間くらいの作業です。

3Dプリンタをお持ちでないかたは3Dhubs、DMM.makeなどに発注すると2週間ほどで届きます。

