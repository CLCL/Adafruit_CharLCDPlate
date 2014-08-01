Adafruit_CharLCDPlate
=====================

Raspberry Pi用Color Backlight Character LCDをPerlで制御するモジュール
Perl library for Adafruit RGB-backlit LCD plate for Raspberry Pi.

## SYNOPSIS

``` perl
use HiPi::Device::I2C;
use HiPi::BCM2835::I2C;
use Adafruit_CharLCDPlate;
use utf8;
use Encode;
 
my $lcd = Adafruit_CharLCDPlate->new();
$lcd->init();
$lcd->begin(16, 2);
$lcd->clear();
$lcd->message("Heiwa na hibi...\nZzz...");
sleep(13);
$lcd->clear();
$lcd->backlight( $lcd->{color}->{RED} );
$lcd->message(encode('cp932', "Apacheｶﾞﾂﾏｯﾀ!\nMaxClients=50"));
sleep(10);
$lcd->clear();
$lcd->stop();
```

## DESCRIPTION

Raspberry Pi用アドオンボード Adafruit RGB-backlit LCD plate は、Raspberry PiからI2C（信号線2本）を介して制御しています。IC2から先は、MCP23017 ポートエキスパンダがつながっており、MCP23017が拡張するGPIOにHD44780互換キャラクタLCDドライバ、LCD組み込みRGBバックライト、入力用タクトスイッチ5個が接続されています。

キャラクタLCDドライバ駆動には、GPIOが7本（7bit、データ通信線4bit＋制御線3bit）あれば可能です。MPC23017 ポートエキスパンダを使う実装は、ArduinoのようにGPIOピンが多い場合はあまり積極的に利用されませんが、Raspberry PiのようなGPIOピンが極端に少ない場合、GPIOピンを節約するという目的で利用されます。また、ポートエキスパンダを利用したことで、キャラクタLCDの表示以外でもRGBバックライトの制御（3bit）、5個のタクトキーからの入力（5bit）が利用できるようになっています。

このような特殊構成のため、製品の制御にはAdafruit Industory製Python libraryが用意されています。これをPerlに移植しました。

## Author

[OONO Yoshitaka ](https://github.com/CLCL/)

## Licence

MIT
