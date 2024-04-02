# Weathers

## 1. このプログラムについて

### 1-1. 練習問題の解答例です

「プログラミングElixir 第２版」<br>
第13章 プロジェクトを構成する

の練習問題の解答例です。

この練習問題は、

https://w1.weather.gov/xml/current_obs/KDTO.xml

で得られる、アメリカ海洋大気庁が提供している気象状況のXMLを取得し、パースして素敵なフォーマットで表示する,
という内容。

これに

> （ヒント：XMLをパースするために、ライブラリをダウンロードする必要はない。）

という謎のヒントが追加されている。

### 1-2. 実装について

基本的に第13章のサンプルプログラムと同じアプローチで実装した。<br>
ただし、XMLをパースするライブラリは使用せず、文字列操作だけで実現した。これは前述のヒントの解釈でもある。

## 2. 使い方

### 2-1. ビルド

ビルド手順を示す。

```sh
$ cd weather
$ mix deps.get
$ mix escript.build
$ ls -F
KDTO.xml   _build/  deps/  mix.exs   test/
README.md  config/  lib/   mix.lock  weathers*
$
```

実行可能なファイル`weathers`が生成されていること。

### 2-2. 実行

コマンドラインから使用する。以下にusageを示す。

```
$ ./wathers <ICAO>
```

<ICAO>はICAD空港コードを指定する。

ICAD空港コード`KDTO`を指定した実行例を以下に示す。

```sh
$ ./weather KDTO
 Title          | Value
----------------+-------------------------------
 Station ID     | KDTO
 Location       | Denton Enterprise Airport, TX
 Weather        | Fair
 Temperature    | 24.4 [C]
 Pressure       | 1015.4 [mb]
 Wind Direction | South
 Wind Speed     | 6.9 [m/h]
$
```

あるいは以下のようにmixコマンドからも使用できる。

```
$ mix run -e 'Weathers.CLI.main(["KDTO"])'
```

### 2-3. ICAO空港コード

上記の**KDTO**はICAO空港コードと呼ばれているもので、ここでは米国内のICAO空港コードが指定できる。


ICAO空港コード<br>
https://ja.wikipedia.org/wiki/空港コード#ICAO空港コード(4レターコード)

米国内の空港のICAO空港コードの例を以下に示す。

* **KJFK** : ジョン・F・ケネディ国際空港（ニューヨーク州）
* **KSFO** : サンフランシスコ国際空港（カルフォルニア州）
* **KDTO** : デントン市営空港（テキサス州）
* **PHNL** : ダニエル・K・イノウエ国際空港（ハワイ州ホノルル）

ちなみに成田国際空港を示す**RJAA**を指定すると、米国管轄でないのでこのプログラムではエラーになる。

以上
