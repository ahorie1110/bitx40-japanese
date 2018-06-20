# インストール・ガイド
このガイドはPE1NWL・Allardさんが作成されたガイドをJJ1EPE・Akiが翻訳したものです。ご質問などがありましたらjj1epe＠jarl.com(＠は小文字)までどうぞ。

## 概要

1. Arduino IDE をPCに[インストール](#Arduino-IDEのインストール)する。

2. [Install](#installing-the-pinchangeinterrupt-library) ライブラリ”PinChangeInterrupt”をPCにインストールする。

3. [Download](#downloading-the-sketch)　Raduinoのスケッチ（ソースコード）をPCにダウンロードする。

4. [Open](#opening-the-sketch) IDEでRaduinoのスケッチを開く。

5. [Compile](#compiling-the-sketch) Raduinoのスケッチsketchをコンパイルする。

6. Bitx40の電源を切る。

7. USBケーブルをRaduinoのUSBポートに接続する。

8. [Upload](#uploading-the-sketch) ファームウエアをRaduinoボードにアップロード（書き込む）する。

9. USBケーブルを外す。

10. Bitx40の電源を入れる。

## Arduino IDEのインストール

Arduino IDE（統合開発環境）は、ソフトウェアを"コンパイル"してArduinoマイクロコントローラチップにアップロード（書き込む）するために必要なソフトウェアです。 Raduinoソフトウェア（または「スケッチ」）はC（プログラミング言語）で書かれています。スケッチ内のプログラム文は、Arduinoマイクロコントローラが理解し実行できるデジタル命令コードに「変換」されていなければなりません。この変換プロセスを「コンパイル」と呼びます。

Arduino IDEソフトウェアは、https://www.arduino.cc/en/Main/Software から無料でダウンロードできます。”Windows Installer, for Windows XP and up”のリンクをクリックしてください。
 
![IDEinstall1](IDEinstall1.png)

次に 'just download'　をクリックします:

![IDEinstall2](IDEinstall2.png)

ダウンロードしたファイルを保存して実行します。 “このアプリで端末を変更できるようにしますか？ ”では「はい」をクリックします。

使用許諾契約に同意します:

![IDEinstall3](IDEinstall3.png)

全てのチェックボックスをそのままの設定にしておき、'Next'　をクリックします:

![IDEinstall3a](IDEinstall3a.png)

保存先フォルダもそのままにしておき　“Install”　をクリックします：

![IDEinstall4](IDEinstall4.png)

インストールが開始され、すべてのファイルを展開してインストールするのに1分ほどかかります：

![IDEinstall5](IDEinstall5.png)

インストールが完了したら“Close”をクリックします：

![IDEinstall6](IDEinstall6.png)

新しくArduinoアイコンがデスクトップに作成されますので、アイコンをダブルクリックしてIDEを起動します：

![IDEinstall7](IDEinstall7.PNG)

IDEが起動します：

![IDEinstall8](jp_IDEinstall8.PNG)

IDEが起動したら、使用言語を日本語に変更します。
"File" => "Preferences"に移動します：

![change-language](jp-change-language.png)

“Editor Language”からプルダウンで“日本語”を選択します：

![change-language2](jp-change-language2.png)

ここで一度IDEを終了し、言語の変更を有効にするために、再起動します：
メニューが日本語に変わります：

次ぎに、書き込むデバイスの選択のために、”ツール”=>”ボード”=> “Arduino Nano”を選択します：

![IDEinstall9](jp_IDEinstall9.png)

次に “ツール”から “プロセッサ“ => “ ATmega328P”を選択します：

![IDEinstall10](jp_IDEinstall10.png)

続いて “ツール”から “書込装置“ => “AVRISP mkii”を選択します：

![IDEinstall11](jp_IDEinstall11.png)

## ライブラリ ”PinChangeInterrupt” のインストール

このスケッチのバージョンでは、割り込み処理のためにライブラリ "PinChangeInterrupt"が必要です[pinChangeInterrupt"](https://playground.arduino.cc/Main/PinChangeInterrupt) 。
これは標準のライブラリではありません（デフォルトではインストールされていません）。 PCにインストールするには、次の手順で行います。
これは１回行うだけです。ult).

1.メニューの　“スケッチ”　から “ライブラリをインクルード” => “ライブラリを管理”　を選択します：

![libray-install1](jp_library-install1.PNG)

2.ライブラリ・マネージャーが起動します。すでにインストールされているライブラリが表示されるまで待ちます：

![libray-install2](https://github.com/ahorie1110/bitx40-japanese/blob/master/installation_instructions/jp_library-install2_a.png)

3.　検索ボックスで "pinchangeinterrupt"　を入力します:

![libray-install3](jp_library-install3.PNG)

4.　“Pin Change Interrupt by NicoHood” という名前のライブラリを選択し、 "インストール" をクリックします:

![libray-install4](https://github.com/ahorie1110/bitx40-japanese/blob/master/installation_instructions/jp_library-install4_a.png)

5.　インストールが完了するまで待ち、完了したら“閉じる”をクリックします：

![libray-install5](https://github.com/ahorie1110/bitx40-japanese/blob/master/installation_instructions/jp_library-install5_a.png)

## スケッチのダウンロード

“github” のページで緑色の "Clone or download"ボタンをクリックします：

![download-sketch1](download_sketch1.png)

'download ZIP'をクリックします:

![download-sketch2](download_sketch2.png)

ファイルは、PCのダウンロードフォルダにダウンロードされます。
ダウンロードフォルダに移動して"bitx40-master"という名前のファイルを探してダブルクリックします：

![download-sketch3](download_sketch3.png)

"展開" をクリックします:

![download-sketch4](download_sketch4_JPN.png)

次に "全て展開" をクリックします:

![download-sketch5](download_sketch5_JPN.png)

必要に応じて、 ”参照”　ボタンを使用して、ファイルが展開される場所を変更します。
次に、"展開"　を押します:

![download-sketch6](download_sketch6_JPN.png)

上の手順で選択した場所に「bitx40-master」という名前の新しいフォルダが作成されます：

![download-sketch7](download_sketch7_JPN.png)

新しく作成されたフォルダ "bitx40-master"には複数のファイルが含まれています。それらの1つは "raduino_v1.27.7.ino"という名前です。これは実際のRaduinoファームウェアです。

![download-sketch8](open_sketch1_JPN.png)

## スケッチを開く

フォルダ "bitx40-master"の中から、ファイル"raduino_v1.27.7.ino"を見つけてダブルクリックします：

![open-sketch1](open_sketch1_JPN.png)

 Arduino IDE が起動します:

![open-sketch1a](jp_IDEinstall8.PNG)

次のメッセージボックスが表示されることがありますが、 OKを押します：

![open-sketch2](jp_open_sketch2.png)

スケッチが開き、プログラムコードがIDEに表示されます：

![open-sketch3](jp_open_sketch3.PNG)

## スケッチのコンパイル

IDEで、下図の“コンパイル” ボタンをクリックします:

![compile-sketch1](jp_compile_sketch1.png)

コンパイルが開始されます。完了するまでに数分かかる場合があります：

![compile-sketch2](jp_compile_sketch2.png)

コンパイルが完了すると、次の画面が表示されます：

![compile-sketch3](jp_compile_sketch3.png)

## スケッチのアップロード（書込み）

最初にBitx40の電源を切ります。
次ぎに、PCのUSBポートとBitx40のUSBポートをUSBケーブルを接続します。
この場合、USBケーブルを介してPCから電源が供給されるため、Raduinoのディスプレイは点灯します。Bitx40自体は動作しません。

 IDE上で下図の ”アップロード” ボタンをクリックします:

![upload-sketch1](jp_upload-sketch1.png)

スケッチは最初に再度コンパイルされますが、これには数分かかることがあります：

![upload-sketch1a](jp_upload-sketch1a.png)

そして、スケッチがArduinoにアップロードされます。これにはもう1分ほどかかります：

![upload-sketch2](jp_upload-sketch2.png)

アップロードが完了しました：

![upload-sketch3](jp_upload-sketch3.png)

Raduinoが再び起動し、新しいファームウェアのバージョン番号がディスプレイに短時間表示されます：

![upload-sketch4](upload-sketch4.png)

USBケーブルを外します：.

Bitx40の電源を入れます。 Raduinoが起動します。
新しいファームウェアをお楽しみください。 Happy BitX-ing！
