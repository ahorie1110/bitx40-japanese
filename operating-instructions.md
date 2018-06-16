## Raduino_v1.27　対応ユーザー説明書　(作成中)

【重要】：このスケッチのバージョンは割込み処理のため ["PinChangeInterrupt"](https://playground.arduino.cc/Main/PinChangeInterrupt)のライブラリが必要です。このスケッチをコンパイルする前に、お使いのIDEにこのライブラリを[インストール](library-install.md)してください。

このバージョンが更新されると、全てのキャリブレーション・データ、ドライブレベル等の設定は全て初期値に設定されます。更新する前に現在のキャリブレーション・データ等を記録しておいてください。更新が完了したら、“ファンクションボタン”を使用して、初期値から記録しておいた設定に戻してください。このスケッチでは基本的なLSBの機能はハードウエアの改造を行わなくても動作します。必要な（最小限の）ハードウエアの改造を行えば、ユーザーの選択により機能を追加して、このソフトウエアにより動作させることができます。それぞれの機能で必要なハードウエアの改造を以下のテーブルに示します。それぞれの改造の詳細は以下を参照してください。

![Table of hardware modifications](https://github.com/ahorie1110/bitx40-japanese/blob/master/hard.jpg)

## 10-TURN TUNING POT
(10回転チューニング・ノブ)(ポテンションメータ)

キットに付属の1回転チューニング・ノブ（ポット）の周波数スパンの初期値は50KHzのみです。
代わりに10回転チューニング・ノブを使用すれば7MHz帯をフルカバーするためにスパンを拡げることができます。

![Image of 10-turn pot hookup](Vishay%20100K%2C%2010-turn%20pot%20wire%20up.jpg)

“ファンクションボタン”を使用して、“SETTINGS”メニューから[希望のポットスパンを設定する](#tuning-range)。

## FUNCTION BUTTON WIRING:
（ファンクションボタンの配線）

モーメンタリー・プッシュボタンをA3ピン（P1コネクタのオレンジ線）とグランドに接続します。Arduinoの内部プルアップ抵抗を使用しますので、外部プルアップ抵抗は必要ありません。

“ファンクションボタン”はまだありませんか？もし、プッシュボタンを使用しない場合には、基本的なLSB機能は動作します（もちろん、この場合にはDual VFO,RIT,USB,CW　などの機能は使えませんが）。但し、キャリブレーションは“CAL”ボタン（P1コネクタのA2ピン、赤線）を使用する従来の方法で行えます。設定幅は34～36行のコードを希望する値に書き換えることよって設定することができます。再コンパイルしてRaduinoにファームウエアを書き込んだら、新しい設定を初期化するために一時的に”CAL”の赤線をグランドに接続します。

## PIN LAYOUT
(ピン配置)
![Raduino pin layout](raduino_pin_layout.png)

### Connector P1 (8 pin)

* A0 (黒): PTTSense
* A1 (茶): Key, "dit"
* A2 (赤): CAL
* A3 (橙): Function Button
* GND (黄色)
* +5V (緑)
* A6 (青): unused
* A7 (紫): Tuning Pot

### Connector P3 (16 pin)

最初の11ピンはヘッダがありません（パッドのみ）：
* D7: TX-RX
* D6: CW Carrier
* D5: CW Side Tone
* D4: CW SPOT Button
* D3: Key, "dah"
* ??: Unused
* ??: Unused
* ??: Unused
* ??: Unused
* ??: Unused
* ??: Unused

５ピンヘッダ

* GND (black)
* GND (brown)
* CLK2 (red)
* +5V (orange)
* ?? (yellow): Unused


his is required for CW operation (or when you want to generate a carrier for tuning)
Connect a wire from Raduino ouput D6 (connector P3, pin 15), via a 4.7K series resistor, to the input of the mixer.

![CW Carrier Wiring](CW-CARRIER%20wiring.png)
## PTT SENSE WIRING:
（PTT検出の配線）
A0ピン（P1コネクタの黒線）を10Kの抵抗を介してBITX40のU3(レギュレータLM7805)の出力に接続します。

![PTT Sense wiring](PTT%20SENSE%20wiring.png)

PTTが押されていないときは（受信モード）、レギュレータはOFFとなりA0ピンは0V（LOW）となります。PTTが押されると（送信モード）レギュレータはONとなりA0ピンは+5V(HIGH)となります。PTT検出は、CW、RIT、SPLITや送信中（“FM-ing”を防ぐ）の周波数変更を行えないようにするために必要です。PTT検出の改造を行なわない場合でも、LSBとUSBでの運用は問題なく動作します。

## CONNECTING A STRAIGHT MORSE KEY or 'TUNE' BUTTON:
（ストレートCWキーまたは“TUNE”ボタンの配線）

ストレート電鍵（または外部エレクトリックキー）をRaduinoのA1ピン（P1コネクタの茶線）に接続することができます。Raduinoの入力を保護するために1Kの抵抗を接続することをお勧めします。キーが押されていない場合（オープン）にはA1ピンは“HIGH”になり、キーが押された場合（クローズ、グランドに短絡）にはA1ピンは“LOW”になり、そしてキャリアが送信されます。

電鍵の代わりにシンプルな押しボタンを接続することもできます。発生されたCWキャリアはアンテナの調整に使用することができます。但し、この場合にはCWキャリアは連続で出力されますのでご注意ください。従って、終段がオーバヒートしないように“TUNE”ボタンを長時間押さないようにしてください。

## AUTOMATIC KEYER - CONNECTING A PADDLE:
（エレキー、パドルの接続）
Raduinoは初期値ではストレート電鍵を使用するよう設定されています。エレキーを使用したい場合には“SETTINGS”メニューで　'CW parameters' => 'Key-type'
and select 'paddle', 'rev. paddle' (左利き用), 'bug', or 'rev.
bug'の順番で選択します。“dit”接点をRaduinoのA1ピン（P1コネクタの茶線）に接続し、“dah”接点をRaduinoのD3ピン（P3コネクタ）に接続します。Arduinoの入力を保護するために、1Kの抵抗を直列につなぐことをお勧めします。内蔵キーヤーは“IambicモードA”と 'bug'モード（Vibroplexエミュレーション）があり、パドルを逆にすることができます。

## ADJUSTING CW KEYER SPEED

The CW keyer speed can be controlled from the front panel (range 1-50 WPM). While keying, press and release the FB to increase the speed, or the SPOT button to decrease the speed. The CW speed setting is memorized in EEPROM.

## CAPACITIVE TOUCH KEYER:
（容量式タッチ・キー）
このスケッチでは容量式タッチ機能をサポートしています。この機能によって、ストレートキーやパドルの代わりにタッチセンターを使用することができます。タッチセンーによってストレートキーや同様にエレキーの運用が可能です。次のURLのYoutubeのデモを見てください：https://www.youtube.com/watch?v=9MWM6UVy9k4

この機能のためには最低限の改造として４つの抵抗を接続する必要があります。注）電源立上げ時にタッチセンサーが正確に動作しないという現象が何件か報告されています。このような場合には、内部のベース静電容量を若干増やすために3～22pFの小さなコンデンサを両方の入力に接続します。

![Capacitive Touch Keyer Mod](capacitive%20touch%20keyer%20modification.png)

初期値では静電式タッチセンサーは無効になっています。タッチセンサーを使用する場合には、“SETTINGS”メニューから'CW parameters' => 'Touch
sensor'を選択し、希望するタッチセンサーの感度をチューニング・ノブで設定します。

タッチセンサーの良好な感度の開始値は“22”です。感度をより高めるには値を上げ、最大値は“25”です。感度の設定はとても繊細で個人の好みにもよります。通常はより高い感度が良い結果を得られます。しかしながら、感度が高すぎると電気的ノイズやタッチパッドの周囲環境によりキーが誤動作してしまうかもしれません。また、１回しかパッドにタッチしていなくても、“スクイズ・キーイング”が生じてしまうかもしれません。一方、感度が低すぎる場合には、タッチパッドの操作にキーヤーが正しく反応せず、例えば“ダブルDITやDAH”が発生してしまうかもしれません。最良の設定を見つけるには少し実験が必要になるでしょう。

タッチセンサーは起動時に自動的にキャリブレーションされます。 再度キャリブレーションしたい場合は、センサパッドに触れないで、単に電源を切ってから再度電源を入れます。
センサーキャリブレーションデータは、起動時にLCDディスプレイに表示されます。注：タッチキーヤーが有効な場合、通常のパドル操作はできません。
標準のパドルを使用する場合は、感度を0（タッチセンサーOFF）に設定してタッチセンサーを無効にします。

## CW-CARRIER WIRING:
（CWキャリアの配線）
CW運用を行うか、アンテナ調整のためのキャリアを発生させたい場合には、この改造が必要です。Raduinoの出力D6（P3コネクタの15ピン）を直列に配線した4.7Kの抵抗を介して、ミキサの入力に配線します。

![CW Carrier Wiring](CW-CARRIER%20wiring.png)

キーが押されているときには出力D6は“HIGH”になります。このとき、ミキサが不平衡になるようにミキサに若干の直流電流が流れます。その結果、CWキャリアが発生します。

注）最大出力時にキャリアが発生しない場合には、ドライブを増加させるために4.7Kの抵抗をより小さな値に変える必要があるでしょう。しかしながら、綺麗なCW信号を発生させるために可能な限り高い抵抗のままとしてください。決して1Kの抵抗は使用しないでください。アンテナ調整のチューニング用だけならば、キャリアは低いほうが望ましいです。この場合、100Kの抵抗を4.7Kの抵抗に直列に接続し、キャリアの強さを適切な強さに抑えることができます。

この“CWキャリア”の改造はCW機能にのみ必要です。この改造を行わなければ、他の機能は問題なく動作します。

## CW SIDE TONE WIRING:
（CWサイドトーンの配線）
サイドトーンはRaduinoのD5出力（P3コネクタの14ピン）より出力できます。サイドトーンは外部オーディオアンプへの出力と並行にスピーカ／ヘッドホンへ出力されます。

![CW Side Tone Wiring](sidetone%20wiring.png)

希望するサイドトーンのピッチは“SETTINGS”メニューの“ファンクション・ボタン”で設定できます。サイドトーンはCW運用のときのみ使用されます。サイドトーンの改造を行わなくても、他の全ての機能は問題なく動作します。

## TX-RX WIRING:
(CW用PTTバイパス配線）

![TX-RX Wiring](TX-RX%20line%20wiring.png)

この改造はCW運用で必要です。

電鍵が押されると出力D7（P3コネクタの15ピン）は“HIGH”になります。電鍵が少なくとも350msの間離れたときのみ出力は再び“LOW”になります（この時間は“SETTINGS”メニューで設定することができます）。出力D7は、CWモードで動作中にPTTのスイッチングをバイパス（無効）するために、PTTスイッチと並列に接続されたNPNトランジスタをドライブするために使用されます。これにより出力D7が“HIGH”の間はリレーが動作します。（ヒント：マイクとPTTを一緒のコネクタにしている場合は、PTTバイパス用トランジスタはその背面に直接はんだ付けできます。PTTバイパス用トランジスタは将来VOX機能を使用する場合にも同様に使用します）

## CW SPOT/FINE TUNE Button:
（CW ゼロ・ビートボタン）

D4ピン（P3コネクタ）とグランドの間にモーメンタリー・プッシュボタンを配線します。Arduinoの内部のプルアップ抵抗を使用しますので、外部のプルアップ抵抗を用いる必要はありません。CWで運用するときには、両方の局が同一の周波数でキャリアを送信することが大切です。受信モードの時に“SPOT”ボタンが押されると、RITがOFFになりサイドトーンが生成されます（キャリアは送信されません）。

“SPOT”ボタンが押されている間、VFOを1Hzの精度にセットできる“FINE TUNE”モードになります。この機能はSSBモードでも同様に使用できます（但しこの場合にはサイドトーンは生成されません）。受信しているCW信号とCWのトーンのピッチが一致するようにチューニング・ポットを調整します。受信しているCW信号のピッチをCWトーンと合わせることにより、自局の信号と他局の信号を完全に同一の周波数にすることができます（ゼロ・ビート）。（“SPOT”とボタンは付加的な機能であって、CW運用で必須の機能ではありません。“SPOT”ボタンがなくても、CW運用は可能です）

## DIAL LOCK FUNCTION
(ダイアル・ロック)

“ファンクションボタン“と“SPOT”ボタンを同時に押すとダイアルをロックすることができます。ダイアルがロックされると“チューニング”ができなくなりますが、PTTとCWは動作します。ロックを解除するには、再び“ファンクションボタン”を押します。

## SPURIOUS BURST PREVENTION
（スプリアス・バーストとの防止）
受信から送信に切り替わる際のスプリアス・バーストの発生を防ぐために、短時間の遅延（TX_DELAY）を設定しています。TX_DELAYは初期値では65msに設定され、必要に応じて71行を変更すればこの遅延時間を調整することができます。

## FUNCTION BUTTON USAGE:
（ファンクションボタンの使用方法）
いくつかの機能はプッシュボタンのみで設定することができます。
必要なハードウエアの改造が行われていない場合には、いくつかのメニューは表示されません。
 
## 運用モード
通常の運用モードの場合：
* 短く１回押す　―　VFO A/Bの切替
* 短く２回押す　―　RIT ON、“ファンクションボタン”を再度押すとRIT OFF
　　　　　　　　　　　　　　　＊この機能を使用するにはPTT検出の改造が必要
* 短く３回押す　―　SPLIT ON/OFFの切替
　　　　　　　　　　　　　　　＊の機能を使用するにはPTT検出の改造が必要
* 短く４回押す　―　LSB-USB-CWL-CWUのモード変更　（ボタンの回転で順番にセレクト）
* 短く５回押す　―　周波数SCANモードの開始
* 短く６回押す　―　VFO　A/Bモニタリングモードの開始
* 長く押す（1秒以上）　―　VFO AとBを同じにする

## 設定モード
“SETTINGS”メニューに入るには３秒以上ファンクションボタンを押します。

## 周波数スキャン
　１回短くボタンを押して周波数SCANのパラメータを設定します（下限、上限、ステップ幅、ステップ遅延）
* チューニング・ノブを使用して、スキャンの下限の周波数を設定する
* ファンクションボタンを押す
* チューニング・ノブを使用して、スキャンの上限の周波数を設定する
* ファンクションボタンを押す
* チューニング・ノブを使用して、スキャンのステップ幅を設定する
* ファンクションボタンを押す
* チューニング・ノブを使用して、スキャンの遅延幅を設定する（A/Bモニタリングモードでも使用）
* ファンクションボタンを押して、設定を記録する。



### Operating Mode

In normal operation mode:

* 1 short press - toggle VFO A/B
* 2 short presses - RIT on (PTT sense is required for this function) (press FB again to switch RIT off)
* 3 short presses - toggle SPLIT on/off (PTT sense is required for this function)
* 4 short presses - switch mode (rotate through LSB-USB-CWL-CWU)
* 5 short presses - start frequency SCAN mode
* 6 short presses - start VFO A/B monitoring mode
* long press (> 1 second) - VFO A=B


### Settings Mode

To enter SETTINGS menu, press and hold the Function Button for a VERY long (>3 seconds).
 
#### Frequency Scan

1 short press sets frequency SCAN parameters (lower limit, upper limit, step size, step delay)

 - using the tuning pot, set the desired lower frequency scan limit
 - press the FB
 - using the tuning pot, set the desired upper frequency scan limit
 - press the FB
 - using the tuning pot, set the desired scan step size
 - press the FB
 - using the tuning pot, set the desired scan step delay (also used for A/B monitoring mode)
 - press the FB again to save the settings

#### CW Configuration

2 short presses - set CW paramaters (sidetone pitch, CW-key type, semiQSK on/off, QSK delay)
   (only available when PTTsense line is installed)

 - using the tuning pot, select "straight" for straight CW key operation, "paddle" for automatic CW keyer,
   "rev. paddle" for left-handed CW-operators, "bug", or "rev. bug".
 - press the FB
 - using the tuning pot, select Auto-space ON or OFF (only when automatic CW keyer was selected)
 - press the FB
 - using the tuning pot, set the desired touch keyer sensitivity (0=OFF) (only when touch sensor mod is installed)
 - press the FB
 - using the tuning pot, select semiQSK ON or OFF (only when TX-RX mod is installed)
 - press the FB
 - using the tuning pot, set the desired timeout value (ms) (only when semiQSK in ON)
 - press the FB again to save the settings
 - using the tuning pot, set the desired sidetone pitch
 - press the FB

#### VFO Calibration, LSB

3 short presses - VFO frequency calibration in LSB mode

  - use another transceiver to generate a carrier at a known frequency (for example 7100.0 kHz)
    (or ask a friend to transmit a carrier at a known frequency)
  - before going into the calibration mode, first set the VFO to 7100.0 kHz in LSB mode
    (the received signal may not yet be zero beat at this point)
  - go into the LSB calibration mode (3 short press)
  - using the tuning pot, adjust the correction value (ppm) for exactly zero beat
  - press the Function Button again to save the setting

#### VFO Calibration, USB
  
4 short presses - VFO frequency calibration in USB mode

  - USB calibration depends on LSB calibration, so make sure that LSB calibration has been done first!
  - use another transceiver to generate a carrier at a known frequency (for example 7100.0 kHz)
    (or ask a friend to transmit a carrier at a known frequency)
  - before going into the calibration mode, first set the VFO to 7100.0 kHz in USB mode
    (the received signal may not yet be zero beat at this point)
  - go into the USB calibration mode (4 short presses)
  - using the tuning pot, adjust the USB offset for exactly zero beat
  - press the Function Button again to save the setting

#### VFO Drive Level, LSB
  
5 short presses - set VFO drive level in LSB mode

  - tune to 7199 kHz, on most BITX40 transceivers a strong birdie is heard in LSB mode
  - give 3 short presses to the FB to enter the VFO drive level adjustment
  - the default drive level in LSB mode is 4mA
  - using the tuning pot, try different drive levels (2,4,6,8 mA) to minimize the strength of the birdie
  - press the FB again to save the setting

#### VFO Drive Level, USB  

6 short presses - set VFO drive level in USB mode

  - tune to a weak signal
  - give 4 short presses to the FB to enter the VFO drive level adjustment
  - the default drive level in USB mode is 8mA
  - using the tuning pot, try different drive levels (2,4,6,8 mA) for maximum signal to noise ratio
  - press the FB again to save the setting
  Extra Note: If the max. drive level of 8mA is still insufficient for USB mode, removal of C91 and C92 may help.
  These caps attenuate the VFO signal at higher frequencies. They're actually only needed for the analog VFO
  and can safely be removed if you use the Raduino DDS instead of the analog VFO.

#### Tuning Range

7 short presses - set tuning range (min frequency, max frequency, pot span)

  - using the tuning pot, set the minimum tuning frequency and press the FB
  - using the tuning pot, set the maximum tuning frequency and press the FB again
  The default pot span is 50 kHz, this is OK for a standard 1-turn pot
  If you install a multi-turn pot instead you can extend the pot span
  - using the tuning pot, set the desired pot span
    recommended value: 50 kHz for a 1-turn pot, 200 kHz for a 10-turn pot
    (if the radio is mainly used for CW: a pot span of 10-25 kHz is recommended)
  - press the FB again to save the setting

#### Exit Settings
 
One long press (>1 second) will exit the SETTINGs menu and return to normal [operating mode](#operating-mode)

All user settings are stored in EEPROM and retrieved during startup.

### Factory Settings

To reset all used settings to "factory" values, press and hold the Function button during power on. The factory settings are:

* VFO calibration value: 0
* VFO calibration offset (USB): 1500 Hz
* VFO drive level (LSB): 4mA
* VFO drive level (USB): 8mA
* Minimum frequency: 7000 kHz
* Maximum frequency: 7300 kHz
* Tuning pot span: 50 kHz
* Mode LSB for both VFO A and B
* CW side tone: 800 Hz
* CW key-type: Straight key
* Touch sensors: OFF
* Auto-space: OFF
* semiQSK: ON
* QSK delay: 350 ms
* Lower scan limit: 7100 kHz
* Upper scan limit: 7150 kHz
* Scan step: 1 kHz
* Scan step delay: 500 ms

A warning message "VFO uncalibrated" will be displayed until you recalibrate the VFO again.
