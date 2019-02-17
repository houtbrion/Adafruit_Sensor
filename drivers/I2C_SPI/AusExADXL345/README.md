# AusExADXL345
このドライバは，
[Adafruitのセンサ統合ライブラリ][AdafruitUSD]を拡張した上で，いろいろなセンサ類を
[統合ライブラリ][AdafruitUSD]のAPIでアクセス可能にするプロジェクトの一部で，
アナログ・デバイセズの[ADXL345 3軸加速度センサ][ADXL345]用のドライバです．
チップは，[Seeed studio][SeedStudio]の[Grove3軸加速度センサ][ProductPage]に
搭載されているだけでなく，[Adafruit][Adafruit]からのモジュールが販売されています．


そのため，[Seeed studio][SeedStudio]，[Adafruit][Adafruit]共に独自の
ドライバを公開しています．

## 仕様

仕様は[チップのページ]を見てね．

[チップのページ]:https://www.analog.com/jp/products/adxl345.html

## ベースとなるコードとライセンス

ベースとなるコードは[Adafruit][Adafruit]の[Githubのプログラム][AdafruitGithub]で，
『BSD Liceense』となっているので，それに従います．
[Seeed studio][SeedStudio]も独自のコードを[公開][github]していますが，[seeed studioのコード]は
Groveの[ProductPage]にあります．


なお，Adafrutiのコードをベースにした理由は以下の2点です．
 - AdafruitのドライバのみSPIをサポートしている
 - 統合するインターフェースはAdaruitのものであるため，Adafruitのコードのほうが変更量が少なくてすむ．

 あと，元のAdafuitのドライバからインターフェース関係以外で変更した主要は部分は以下の通りです．
 - ハードウェアSPIのサポート
 - I2Cの場合に，I2Cのアドレスを指定する機能を削除

 ハードウェアSPIを利用する場合は，クラスのオブジェクトを生成する際に，ソフトウェアSPIの
 インターフェース(全てのピンを指定する)を利用してもらい，クロックピンの番号を「-1 (0xFF)」に
 してもらえば，ArduinoのハードウェアSPIインターフェースを利用します．

 ESP32のように，SPIのインターフェースが「SPI, SPI1」とか複数ある場合は「SPIのみ対応」となります．
 

## 動作検証

手元にあるADXL345のモジュールがGroveのモジュールしかないため，
SPIは一部を除いて未確認．

|CPU| 機種 |ベンダ| I2C | ソフトSPI | ハードSPI | 備考 |
| :--- | :--- | :--- | :---: | :---: | :---: |:--- |
|AVR| [Uno R3][Uno]  |[Arduino][Arduino]|     | | |      |
|       | [Mega2560 R3][Mega] |[Arduino][Arduino] |  ○  | |   |      |
|       | [Leonardo Ethernet][LeonardoEth] |[Arduino][Arduino] |○   | |  |      |
|       | [Pro mini 3.3V][ProMini] | [Sparkfun][Sparkfun] | ×   | | |      |
| ARM/M0+ | [M0 Pro][M0Pro] |[Arduino][Arduino] |○||||
|ESP8266|[ESPr developer][ESPrDev]| [スイッチサイエンス][SwitchScience] |○|||起動からセンサ値読み取り可能まで数秒必要|
|ESP32 | [ESPr one 32][ESPrOne32] | [スイッチサイエンス][SwitchScience] |○|○|○|SPI接続を確認したのはESPr one 32ではないが，ここにまとめて記載|

## 外部リンク

- Seeed Studio技術Wiki [http://wiki.seeedstudio.com/Grove-3-Axis_Digital_Accelerometer-16g/][SeedWiki]
- センサ商品ページ [https://www.seeedstudio.com/Grove-3-Axis-Digital-Accelerometer-16-p-1156.html][ProductPage]
- Seeed Studioソースリポジトリ [https://github.com/Seeed-Studio/Accelerometer_ADXL345][github]
- Adafruitソースリポジトリ [https://github.com/adafruit/Adafruit_ADXL345][AdafruitGithub]
- Adafruit Unified Sensor Driver - [https://github.com/adafruit/Adafruit_Sensor][AdafruitUSD]
- Groveシールド - [https://www.seeedstudio.com/Base-Shield-V2-p-1378.html][shield]
- Arduino M0 Pro - [https://store.arduino.cc/usa/arduino-m0-pro][M0Pro]
- Arduino Due - [https://store.arduino.cc/usa/arduino-due][Due]
- Arduino Uno R3 - [https://store.arduino.cc/usa/arduino-uno-rev3][Uno]
- Arduino Leonardo Ethernet - [https://store.arduino.cc/usa/arduino-leonardo-eth][LeonardoEth]
- Arduino Mega2560 R3 - [https://store.arduino.cc/usa/arduino-mega-2560-rev3][Mega]
- Arduino Pro mini 328 - 3.3V/8MHz - [https://www.sparkfun.com/products/11114][ProMini]
- ESPr developer - [https://www.switch-science.com/catalog/2652/][ESPrDev]
- ESPr Developer用GROVEシールド - [https://www.switch-science.com/catalog/2811/][ESPrDevShield]
- ESpr one - [https://www.switch-science.com/catalog/2620/][ESPrOne]
- ESPr one 32 - [https://www.switch-science.com/catalog/3555/][ESPrOne32]
- Grove - [https://www.seeedstudio.io/category/Grove-c-1003.html][Grove]
- Seed Studio - [https://www.seeedstudio.io/][SeedStudio]
- Sparkfun Electronics - [https://www.sparkfun.com/][Sparkfun]
- スイッチサイエンス - [https://www.switch-science.com/][SwitchScience]

<!-- 以下は，外部リンクの定義 -->
[Grove]:https://www.seeedstudio.io/category/Grove-c-1003.html
[ADXL345]:https://www.analog.com/jp/products/adxl345.html
[SeedStudio]:https://www.seeedstudio.io/
[Adafruit]:https://www.adafruit.com/
[ProductPage]:https://www.seeedstudio.com/Grove-3-Axis-Digital-Accelerometer-16-p-1156.html
[SeedWiki]:http://wiki.seeedstudio.com/Grove-3-Axis_Digital_Accelerometer-16g/
[github]:https://github.com/Seeed-Studio/Accelerometer_ADXL345
[AdafruitGithub]:https://github.com/adafruit/Adafruit_ADXL345
[AdafruitUSD]:https://github.com/adafruit/Adafruit_Sensor
[shield]:https://www.seeedstudio.com/Base-Shield-V2-p-1378.html
[M0Pro]:https://store.arduino.cc/usa/arduino-m0-pro
[Due]:https://store.arduino.cc/usa/arduino-due
[Uno]:https://store.arduino.cc/usa/arduino-uno-rev3
[Mega]:https://store.arduino.cc/usa/arduino-mega-2560-rev3
[LeonardoEth]:https://store.arduino.cc/usa/arduino-leonardo-eth
[ProMini]:https://www.sparkfun.com/products/11114
[ESPrDev]:https://www.switch-science.com/catalog/2652/
[ESPrDevShield]:https://www.switch-science.com/catalog/2811
[ESPrOne]:https://www.switch-science.com/catalog/2620/
[ESPrOne32]:https://www.switch-science.com/catalog/3555/
[Grove]:https://www.seeedstudio.io/category/Grove-c-1003.html
[SeedStudio]:https://www.seeedstudio.io/
[Arduino]:http://https://www.arduino.cc/
[Sparkfun]:https://www.sparkfun.com/
[SwitchScience]:https://www.switch-science.com/

<!--- コメント
[Adafruit Unified Sensor Driver][AdafruitUSD]
[Groveシールド][shield]
[Arduino M0 Pro][M0Pro]
[Arduino Due][Due]
[Arduino Uno R3][Uno]
[Arduino Mega2560 R3][Mega]
[Arduino Leonardo Ethernet][LeonardoEth]
[Arduino Pro mini 328 - 3.3V/8MHz][ProMini]
[ESpr one][ESPrOne]
[ESPr one 32][ESPrOne32]
[Grove][Grove]
[Seed Studio][SeedStudio]
[Arduino][Arduino]
[Sparkfun][Sparkfun]
[スイッチサイエンス][SwitchScience]
--->
