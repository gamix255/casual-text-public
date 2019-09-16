## 個人的なATmega328P単品をArduinoIDEで開発する際の記録（書き込み手順）

### 個人的なメモです。最適でないところがいろいろあります。

#### 前提条件
- WindowsPCを使った時の記録。Windows10 pro 1903
- スケッチのビルドにはarduino-1.8.10-windows.zipを利用。
- ブレッドボードと単品のATmega328pを利用。
- USBから書き込み時のハードウェアとしてFTDI Basic(3.3V版)を利用。
- 書き込み時のソフトウェアとして、avrdude-serjtag04nを利用。
- Bootloaderは使わない。
- fueseはすでに書き込み（設定？）済み

これまでのストーリー  
Arduino Pro(ATmega168のもの)しかもっていないために、容量と単価の兼ね合いで
ブレッドボードでATmega328Pを愛用？していた。定期的にしかArduinoを使わないために、
時々書き込み手順が分からなくなる。（PCが変わったり、PCのOSが変わったり、各種ソフトのバージョンが変わる。）
今の時点での書き込み可能な手順を確認してみた。


```
現状のfuse
avrdude: safemode: lfuse reads as E2
avrdude: safemode: hfuse reads as DA  
avrdude: safemode: efuse reads as 7  
```

### 準備（ソフトウェアのダウンロードとDLLの配置）
- ArduinoIDEをダウンロードしてくる。記事の時点では、1.8.10だった。
- avrdude-serjtag04nを展開する。

avrdude-serjtag04n付属のavrdudeを実行すると、libusb0.dllが足りない。このファイルはArduinoIDEの方から持ってきておく。
<details>
<summary> 失敗した箇所（ソフトウェア選びの時点）
 </summary>
<p>
avrdude-serjtagを使わなくてよくなったという記述をいろいろなところで見た。しかし、<br>
<code>
avrdude: error: no libftdi or libusb support. Install libftdi1/libusb-1.0 or libftdi/libusb and run configure/make again
</code><br>
となるため、あきらめてavrdude-serjtag04n付属のavrdude.exeを使った。
</p>
</details>

### 配線
下記の通りに配線  
*(後でもう少し詳しく)*
```
DTR RESET pin1
CTS D13 pin19
TXO D11 pin17
RXI D12 pin18

Power VCC pin7
Power AVCC pin7
GND GND pin8 
GND A0 pin23

```

### ボード情報のIDEへの追加

https://www.arduino.cc/en/Tutorial/ArduinoToBreadboard
から、ファイルをダウンロードしてそのまま使えるような記述が色んなところにあるけれど、
1.6.xまでの定義ファイルしかないため、ファイル内の行が1行足りなかった。  

https://github.com/oshlab/Breadboard-Arduino 
を参考にボードマネージャーの追加画面から次の行を追加した。
```
https://raw.githubusercontent.com/oshlab/Breadboard-Arduino/master/avr/boardsmanager/package_oshlab_breadboard_index.json
```

### スケッチからhexファイルを得る
スケッチ→コンパイルしたバイナリを出力

### avrdue-serjtagでの実際の書き込み手順
```
実際の書き込み手順
avrdude -v -patmega328p -c breakout -Pft0 -B19200 -U flash:w:sketch_sep16a.ino.arduino_standard.hex
```


参考
- https://www.arduino.cc/en/Tutorial/ArduinoToBreadboard
