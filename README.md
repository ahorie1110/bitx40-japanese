# bitx40 - Japanese text version by Akira JJ1EPE

# Bitx40 Raduio用スケッチ

このスケッチは、改造されていないBITX40 + raduinoボードであっても、常に動作する汎用の標準Raduinoソフトウェアを目的とししています。 ハードウエアを変更することなく、このスケッチは標準かつ基本的なLSB機能を提供します。 このスケッチは、USB、CW、RIT / SPLIT、KEYERなどの追加機能を提供しますが、これらは関連する（最小限の）ハードウエアの改造が行われた場合のみに機能します。

![Hardware mod overview](hardware%20modification%20overview.PNG) 

詳細は["operating-instructions.md"](operating-instructions.md) と[”software installation instructions"](installation_instructions/0-software-installation.md) を参照してください。

**Note 1:** v1.20以降、SI5351ライブラリをダウンロードしてインストールする必要がなくなったため、 現在はSI5351を駆動するための最小限のルーチンがス　ケッチに組み込まれています。
**Note 2:** v1.27以降、ライブラリ[”PinChangeInterrupt”](https://playground.arduino.cc/Main/PinChangeInterrupt) は割込み処理に必要になりました。コンパイルする前にIDEにこのライブラリを[インストール(library-install.md)してください。

#ご寄付のお願い

私は、趣味としてのアマチュア無線のソフトウェアを開発してアップデートし、そして無料で配布しています。
もし、このソフトウェアを気に入っていただけましたら、知的障害や自閉症の子供のための施設に滞在している私の息子の家に小額でも結構ですのでご寄付いただければ幸いです。ご寄付いただいた浄財は、改良されたおもちゃ、三輪車、トランポリンまたはスイング等に使用させていただきます。このグループの6人の青少年から心より感謝致します。

 [![ご寄付](https://www.paypalobjects.com/en_US/GB/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=PTAMBM6QT8LP8)

# アップデート履歴

v1.27.7
- “PTTsense”モードが実装されている場合にのみ“割り込み”が有効になるようにコードを若干修正した。

v1.27.6
- 周波数が上限または下限に達した場合には、si5351が受信周波数のチューニング動作を継続しないとようにコードを改善した。
- semiQSKがONのときにCWL/ CWUのモード切り替えが正しく行われなかった不具合を修正した。
- より操作しやすいように“ファンクションボタン”の遅延時間の初期値を大きくした。
- “CW-CARRIER”モードで手順を更新した。CWで最大出力が出るように10Kの代わりに4.7Kの抵抗を使用してください。

v1.27.5
- 33行目：高速チューニングの“ステップ遅延時間”を設定する機能を追加した（チューニング・ノブが上限/下限の位置にあるとき）（tks Bob、N4FV）

v1.27.4
- 行32：LCDの2行目にブランクの場合にはテキスト（例：コールサイン）を表示する機能を追加した（tks Richard、VE3YSH）。
- コードの若干の整理

v1.27.3
- si5351の25MHz水晶の負荷容量の設定を修正した（tks Daniel KB3MUN）。
- キャリブレーションの初期値を180 ppmに変更した。

v1.27.2
- “QSK DELAY”タイムが短いと、CWからSSBモードに復帰しなかったバグを修正した（テストの協力tks　Gary N3GO　）

v1.27.1
- CW-SPLITモードでスプリアスキャリアバーストが抑制されなかったバグを修正。
- semiQSKモードでは、キャンセルされずに（キャリアバーストを防止するために）、最初のCWエレメントを65msの遅れに設定した。
- semiQSKモードで無線機がLSBからCWLに確実に切り替わらなかった不具合を修正した。
- VFOが10MHz以上になるとディスプレイの表示に不具合が生じるバグを修正した。

v1.27
- RXからTXへの切り替え時にスプリアスキャリアの抑制を改善した。この関数は、割り込み処理のためにライブラリ[ “PinChangeInterrupt”](https://playground.arduino.cc/Main/PinChangeInterrupt)が必要である。 本スケッチをコンパイル編集する前にIDEを使って[インストール](library-install.md)する。

v1.26
- メニューの構成を整理し、必要なハードウエアの改造が行われていない場合には、それに関連するメニューをスキップするようにした。
- TXに切り替わると、スプリアスキャリアバーストを抑制するようにした（tksDave M0WID）。
- VFOキャリブレーションでは、広範囲の周波数レンジでの精度向上のために“倍率補正”（ppm）を使用するように改良した(tks Jerry KE7ER)。
- EEPROMへのユーザー設定のセーブ/リストア方法をの改良した(tks Pavel CO7WT）。

v1.25.1
- タッチキーヤー・キャリブレーションの若干の不具合を修正した。

v1.25
- 容量式タッチキーヤーのサポートを追加した。

v1.24
- よりスムーズなキーイングのためにCWキーのタイミング特性を最適化した（tkHidehiko、JA9MAT）。
- ダイヤルロック機能を追加した：ファンクションボタンとSPOTボタンを同時に押すと、ダイヤルがロックされる。もう一度ファンクションボタンを押すとロックが解除される。

v1.23.1
- EEPROMのロケーションの誤りによって”auto-space”の設定が「最大周波数」の設定により妨げられる不具合を修正した。
- CWキーが押されたときの、SETTINGSメニュー（CWパラメータ）での表示の不具合（乱雑に表示される）を修正した。

v1.23
- “SETTINGS”メニューでCWキーの”auto-space”機能の有効と無効の切替ができるように改良した（初期値の設定はOFF）。
- Vibroplexのバグ・エミュレーションをCWキーヤーに追加した。
- ユーザー設定パラメータを任意に変更できるように全ての設定パラメータをスケッチの最上部に移動した。
- キーヤー・ルーチンのコードを最適化した（tks Pavel CO7WT)）。

v1.22
- “SETTINGS”メニューから、「パドル」または「反転パドル」を選択できる機能を追加した。

v1.21
-エレキーの機能を追加した。CWキーの初期値はストレートキー。エレキーを使用する場合は、ピンA1（dit）とピンD3（dah）にパドルキーヤーを接続する。“SETTINGS”メニューで、CWキーのタイプを「パドル」に設定する。キーイング中に、ファンクションボタン（早くする）またはSPOTボタン（遅くする）を押すと、キーヤースピードを調整できる。キーヤー速度は1〜50 WPMの幅で設定できる。
- “SETTINGS”メニューでチューニングできる最大周波数と最小周波数の設定できるようにした（スケッチを編集する必要はなくなった）。
- チューニング・ノブの最大位置と最小位置での反応を改善した。


v1.20.1
- Added some constraints so that frequency limits are respected during fast up/down scanning

v1.20
- Embedded Jerry Gaffke's, KE7ER, "minimalist standalone si5351bx routines". This not only makes the sketch independant from an
  external SI5351 library, but it greatly reduces the memory usage as well. The program space is needed for future development
  of additional features that would otherwise not fit in a Nano. Thanks Jerry!

v1.19
- Improved responsiveness of the tuning pot for smoother tuning (less need to fiddle up and down to set the correct frequency)
- Improved "Fast Tune" (at either ends of the tuning pot).
  The step size is now variable: the closer to the pot limit, the larger the step size.
- In CW SPOT tuning mode, short side tone pulses will be generated instead of a continuous tone.
  This makes SPOT tuning easier when tuning to weak CW signals.
- Calibration can now done at 1 Hz precision

v1.18
- improved CW performance at higher CW speeds:
  reduced the delay at the start of CW transmissions (first dit is no longer lost at high speed CW)
  optimized code so that 1:3 CW-ratio is kept even at high CW speed
- improved FINE TUNE mode so that exact frequency (at 1 Hz precision) is displayed while the SPOT button is held pressed
- added an extra option in the SETTINGS menu for setting semiQSK ON or OFF.
  This may be useful for CW operators who want to manually activate the PTT (e.g. using a foot switch).
  if semiQSK is ON:
    radio will automatically switch to CWL (or CWU), and go into TX mode when the morse key goes down
    go back to RX automatically when the QSKdelay time is exceeded
    radio will switch back to LSB (or USB) when the operator presses the PTT switch
  if semiQSK is OFF:
    operator must activate PTT manually to move the radio in TX
    pressing the PTT does not affect the mode. Use the Function Button to select the desired mode (LSB-USB-CWL-CWU)
- corrected a bug that FINE TUNE was not properly applied in USB mode

v1.17.1
- corrected a bug in v1.17 in the shiftBase() routine that the radio didn't return to the correct frequency after switching 
  VFO's, RIT, SPLIT, FINE TUNE etc.

v1.17
- Added "Fine Tune" capability to SPOT button
  While the SPOT button is held pressed, the radio will temporarily go into "FINE TUNE" mode, allowing the VFO to be set at 1Hz 
  precision. This feature works also in SSB mode (except that no sidetone will be generated then).

v1.16
- Added CW SPOT TONE button for exact zero beating.
  Connect a pushbutton to Arduino pin D4. A SPOT tone will be heard when D4 is connected to ground.
  By aligning the CW Spot tone to match the pitch of an incoming station's signal, you will cause your signal and the
  other station's signal to be exactly on the same frequency (zero beat).

v1.15.1
- RIT offset should only be applied during RX. Due to a small bug the RIT offset was not turned off during transmitting CW.
  (RIT in SSB was OK). This has been corrected - RIT works correctly now in all modes.

v1.15
- Added true RIT functionality (adjustable RX offset while TX frequency remains fixed) (2 Function Button presses)
- The old 'RIT' function, based on switching between VFOs A/B, is now called "SPLIT" (3 presses)
- Mode selection (4 presses) now rotates between LSB-USB-CWL-CWU
- Major code cleanup to reduce memory usage
- Inserted some delay in various routines to prevent annoying buzzing sound in SETTINGS menu

v1.14.1
- Corrected small bug in v1.14 that caused slight ticking noise when the radio was left idle.

v1.14
- added VFO A/B monitoring mode (press Function Button 5 times)
- use RX-offset instead of TX-offset in CW mode - the display now shows the correct TX frequency in CW
- changed the way to switch from CW to SSB mode: press PTT to return to SSB mode (tks Willy W1LY)
- restored the functionality for old way calibration method
- simplified the method for sidetone setting: hold key down to hear sidetone
- improved the display during "fast scan" at tuning pot limits (tks Paul KC8WBK)

v1.13
- added frequency scanning capability
- added functionality so that the user can set the CW timout value via the SETTINGS menu
- added decimal point to the VFO for better readability, like so: A 7.123.4 LSB
- simplified calibration routine and cleaned up the code to preserve memory space 

v1.12
- improved responsiveness of Function Button for better user experience
- corrected Tuning Range and SideTone setting procedures

v1.11
- added menu beeps (needs CW sidetone to be wired up)
- corrected a minor bug that "TX" is always shown when PTT-SENSE line has not been installed

v1.10
- added CW functionality (for straight morse key). This function can also be used just for tuning up.
  This requires the CW-CARRIER line connected to Raduino output D6 (connector P3, pin 15).
  (see https://github.com/amunters/bitx40/blob/master/CW-CARRIER%20wiring.png for wiring instructions).
  The morse key itself shall be connected to Raduino pin A1 (brown wire).
  Both sidebands (CWU or CWL) are available for CW operation.
- Semi break-in for CW
  This requires the TX-RX line from Raduino output D7 (connector P3, pin 16) to override the existing PTT
  switch using a NPN transistor. 
  (see https://github.com/amunters/bitx40/blob/master/TX-RX%20line%20wiring.png for wiring instructions)  
- CW side-tone
  This requires some wiring from Raduino output D5 (connector P3, pin 14) to the speaker.
  (see https://github.com/amunters/bitx40/blob/master/sidetone%20wiring.png for wiring instructions).
  The desired sidetone pitch can be set using the Function Button in the SETTINGS menu.
- Frequency tuning is disabled during TX (to prevent flutter or "FM-ing" during TX).
  This requires the PTT SENSE line connected to pin A0 (black wire).
  (see https://github.com/amunters/bitx40/blob/master/PTT%20SENSE%20wiring.png for wiring instructions).

v1.09
- added RIT (SPLIT) functionality. This requires a PTT sense line connected to pin A0 (black wire)
  (see https://github.com/amunters/bitx40/blob/master/PTT%20SENSE%20wiring.png for wiring instructions)
- simplified tuning range setting in SETTINGS menu
- less frequent EEPROM writes so that EEPROM will last longer

v1.08
- mode (LSB or USB) of each VFO A and B is now also memorized
- the BITX status (VFO frequencies, modes) is now stored in EEPROM every 10 seconds and retrieved during start up
- a warning message "uncalibrated" is displayed when calibration data has been erased

v1.07
- Added functionality via the Function Button:
  Use a pusbutton to momentarily ground pin A3 (orange wire). Do NOT install an external pull-up restistor!
- dual VFO capability (RIT is not yet working though)
- LSB/USB mode
- Settings menu for calibration, tuning range, VFO drive level
- All settings are stored in EEPROM and read during startup

v1.06
- no functional changes in this version, only improved the updateDisplay routine (Jack Purdum, W8TEE)
  (replaced fsprint commmands by str commands for code space reduction)

v1.05
- in setup(): increase the VFO drive level to 4mA to kill the birdie at 7199 kHz (Allard, PE1NWL)
  (4mA seems the optimum value in most cases, but you may try different drive strengths for best results -
  accepted values are 2,4,6,8 mA)

v1.04
- Sketch now allows the (optional) use of a 10-turn potentiometer for complete band coverage (Allard, PE1NWL)
- Standard settings are still for a 1-turn pot.
- But if you want to use a 10-turn pot instead, change the values for 'TUNING_RANGE' and 'baseTune'
  in lines 189 and 190 to your liking
  
v1.03
- improved tuning "flutter fix" (Jerry, KE7ER)

v1.02
- fixed the calibration routine (Allard, PE1NWL)
- fetch the calibration correction factor from EEPROM at startup (Allard, PE1NWL)
- added some changes to comply with si5351 library v2. (Allard, PE1NWL)

v1.01
- original BITX40 sketch (Ashhar Farhan)

