================================================================
はじめに：
================================================================
MSX版THE HOBBITのカセットテープから
データを読み取り、ディスクに保存し、
実行するプログラムです。

================================================================
環境：
================================================================

要MSX2VRAM128KB/RAM64KB以上
要DISKドライブ
要カセットインターフェース・データレコーダ

================================================================
使い方：準備
================================================================

■ カセットテープからディスクにデータを移す

まずTAPE-IN.BASを実行します。
TAPE-IN.BASはF1キーにマシン語呼び出しをセットして
すぐBASICに戻ります。（Okと表示されます）

テープを巻き戻し、テープの準備が済んだら、再生と同時に
F1キーを押してください。

（※ ご注意 ※
　　この時、SCREEN0のWIDTH80や漢字画面の場合に、
　　読み取った結果がおかしくなります。

　　TAPE-IN.BASはVRAMの64KB以降にデータを読むのですが、
　　SCREEN0のWIDTH80はVRAMのマッピングが異なるので
　　画面が化けます。

　　漢字モードは純粋にグラフィックモードだからです。）

■ 読み捨て１

まず

a=user(0)
- ASCII -
FILENAME：HOBBIT

と表示された後、しばらく読み込み、

DATA:VRAM 10000H-1????H
Ok

と出て、BASICに戻ります。
（※正確なアドレスは記憶があやふや）
これはテキスト形式のBASICプログラムなので無視します。

■ 読み捨て２

続けてF1キーを押してください。

a=user(0)
- BLOAD -
FILENAME：HOBBIT

と表示された後、しばらく読み込み、

HEAD:????H
 END:????H
  GO:????H
DATA:VRAM 10000H-1????H
Ok

と出て、BASICに戻ります。
（※正確なアドレスは記憶があやふや）

これは先ほどのHOBBITというBASICプログラムから読み込まれる
マシン語プログラムで、ローダー部分に相当します。
こちらも使用しないので無視します。

■ 必要なデータの保存と結合

続けてF1キーを押してください。

a=user(0)
- OTHER DATA -

と表示された後、かなり長い間読み込み、

DATA:VRAM 10000H-1????H
Ok

と表示されます。

◎ これは、タイトル画面、ゲーム本体などのバイナリデータです。
◎ 表示されたアドレスをメモしてください。
◎ 何個か（5個ぐらい？）に分かれると思うのですが
　 いったん一つずつ保存して、後で結合するなどしてください。
　 全体で74KBぐらいなので、VRAM上で結合できます。

● 保存方法：

SCREEN5:SETPAGE2,2:BSAVE"HOBBIT☆.DAT",0,&H????,S

	（☆の部分は任意の連番にしてみてください）
	（????は先ほどメモした終了アドレスの下4桁部分です）

	と、一気に入力してリターンキーを押してください。

	また、結合するときに使うのでセーブしたアドレスをメモします。
	（同梱のFILEADRS.BASでBSAVEファイルヘッダ後から調べることも出来ます）


● データは何個かに分かれていますので繰り返します。

● すべてデータを保存したら、
（手抜きな説明ですみません）

先ほど保存したファイルを
VRAMに順番に並べてから
"HOBBIT.DAT"として保存してください。

（今ならPC上で結合しても良いですが、
　いったんBSAVEしたものなので、
　ヘッダを取り除いてから結合する必要があります。）

自分は当時、手作業で計算してやったのですが、
よく考えたらプログラムを作っておけばよかったなと思います。

================================================================
使い方：実行
================================================================

HOBBIT.DATが準備できたら
RUN"HOBBIT.BAS"
を実行するだけです。
タイトル画面の出方も、テープオリジナルと近いように再現しています。

ただし、セーブデータの保存と読み込みはテープが必要です（笑）

キーマトリクスをゲームでは直接読み込んでいるので、
ハックして割り込んで何か特殊な処理でBASICに戻るなどの改造が
当時の自分では出来ませんでした。


================================================================
ファイル説明：
================================================================

HOBBIT.ASF		ローダーのアセンブラソース
				残念ながら、メイン部分のみで細かいサブルーチンは
				ソースを紛失しています。
HOBBIT.BOF		ローダーの実行バイナリ。HOBBIT.BASから使います。
HOBBIT.BAS		HOBBIT.DATを読み込んで実行します。

FILEADRS.BAS	BSAVEされたファイルのヘッダを読み込んで
				先頭アドレスや終了アドレスを表示します

その他：

MSX2ASM			MSX2用のシンプルアセンブラ、出典はバッ活の投稿作品。
MSX2ASM.BIN		BLOAD"MSX2ASM.BIN",r もしくは RUN"MSX2ASM"でアセンブラモードに
				アセンブラモードになったら
				_ASM("ファイル名    ※拡張子除く
				で。???.ASFを読み込んでアセンブルします。
				*.ASFはテキストファイルです

その他は実験プログラムや共通サブルーチン集です。
物好きな方向け。

