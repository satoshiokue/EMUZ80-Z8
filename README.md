# EMUZ80-Z8

![Z8 Prototype2](https://github.com/satoshiokue/EMUZ80-Z8/blob/main/imgs/IMG_1499.jpeg)  
ブレッドボード試作 シリアル通信試行

![Z8 Prototype](https://github.com/satoshiokue/EMUZ80-Z8/blob/main/imgs/IMG_1497.jpeg)  
ブレッドボード試作

電脳伝説さん(@vintagechips)のEMUZ80が出力するZ80 CPU信号をメザニンボードで組み替え、Z8を動作させることができます。  
Z8とPIC18F47Q43の組み合わせで動作確認しています。

動作確認で使用したCPU  
Z86C9116PSG  
Z8681PS

ソースコードはGazelleさんのEMUZ80用main_cpz.cを元に改変してGPLライセンスに基づいて公開するものです。

https://drive.google.com/drive/folders/1NaIIpzsUY3lptekcrJjwyvWTBNHIjUf1

## メザニンボード
https://github.com/satoshiokue/MEZZ8

## 回路図
https://github.com/satoshiokue/MEZZ8/blob/main/MEZZ8.pdf

## ファームウェア

EMUZ80で配布されているフォルダemuz80.X下のmain.cと置き換えて使用してください。

## アドレスマップ
```
ROM   0x0000 - 0x07FF
     (0x0800 - 0x1FFF) ROM GHOST 0x0000 - 0x07FF
RAM   0x4000 - 0x4FFF  

ROM   0xF000 - 0xFFFF  ROM GHOST 0x0000 - 0x00FF :NMOS Boot
```

0xF000のROM GHOSTはNMOS Z8が起動するときにアクセスする領域です。  
CMOSのZ8はアドレスバスA15-A8が有効な状態で起動して、0x000C番地から命令を実行します。  
NMOSのZ8はアドレスバスA15-A8は「入力ポート・ハイインピーダンス」で起動し、Z8が自分でアドレスバスに設定変更します。ハイインピーダンスの信号線はPIC内蔵プルアップ抵抗によって0xFF--となります。Z8が0x000C番地のメモリをアクセスするとPICの0xFF0Cがアクセスされ、ROM GHOSTの0x000Cにあるデータが渡されます。

## Z8プログラムの改編
バイナリデータをテキストデータ化してファームウェアの配列rom[]に格納するとZ8で実行できます。

テキスト変換例
```
xxd -i -c16 foo.bin > foo.txt
```

## 謝辞
思い入れのあるCPUを動かすことのできるシンプルで美しいEMUZ80を開発された電脳伝説さんに感謝いたします。

## 参考）EMUZ80
EUMZ80はZ80CPUとPIC18F47Q43のDIP40ピンIC2つで構成されるシンプルなコンピュータです。

![EMUZ80](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_Z80.jpeg)

電脳伝説 - EMUZ80が完成  
https://vintagechips.wordpress.com/2022/03/05/emuz80_reference  
EMUZ80専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-051.html

## 参考）phemu6809
comonekoさん(@comoneko)さんがEMUZ80にMC6809を搭載できるようにする変換基板とファームウェアphemu6809を発表されました。

![phemu6809](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_6809.jpeg)

https://github.com/comoneko-nyaa/phemu6809conversionPCB  
phemu6809専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-056.html
