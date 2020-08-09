# DOS で遊ぶ
## FreeDOS を QEMU でインストールする
```bash
$ brew install qemu
$ qemu-img create -f qcow2 freedos.img 500M
$ wget http://www.freedos.org/download/download/FD12CD.iso
$ qemu-system-i386 freedos.img -cdrom FD12CD.iso -boot d
```

![](img/000.png)

"Install to harddisk" を選択

![](img/001.png)

"English" を選択

![](img/002.png)

"Yes - Continue with the installation" を選択

![](img/003.png)

"Yes - Partition drive C:" を選択

![](img/004.png)

"Y" を選択

![](img/005.png)

"1" (Craete DOS partition or Logical DOS Drive) を選択

![](img/006.png)

"1" (Create Primary DOS Partition) を選択

![](img/007.png)

"Y" を選択

![](img/008.png)

"Esc" を選択

![](img/009.png)

"Ecs" を選択

![](img/010.png)

"Ecs" を選択

![](img/011.png)

"Yes - Please reboot now" を選択

![](img/012.png)

"Install to harddisk" を選択

![](img/013.png)

"English" を選択

![](img/014.png)

"Yes - Continue with the installation" を選択

![](img/015.png)

"Yes - Please erase and format drive C:" を選択

![](img/016.png)

"Enter" を押下

![](img/017.png)

"US English (Default)" を選択

![](img/018.png)

"Full installation" を選択

![](img/019.png)

"Yes - Please install FreeDOS 1.2" を選択

![](img/020.png)

インストールが完了するまで待つ

![](img/021.png)

"Yes - Please reboot now" を選択

![](img/022.png)

"Boot from system harddisk" を選択

![](img/023.png)

"1 - Load FreeDOS with JEMMEX, no EMS (most UMBs), max RAM free" を選択

![](img/024.png)

起動完了！

次回以降は、以下のコマンドで起動できる。
```bash
qemu-system-i386 freedos.img -boot c
```

### Links
- [FreeDOS を QEMU で動かす](https://blog.tiqwab.com/2018/10/01/freedos.html)
- [Install Howto - FreeDOS](http://wiki.freedos.org/install/)





## MS-DOS を QEMU でインストールする
まずは[ここ](https://winworldpc.com/download/c38fc38d-68c2-bbe2-80a6-4b11c3a4c2ac/from/c39ac2af-c381-c2bf-1b25-11c3a4e284a2)から、Microsoft MS-DOS 6.22 Plus Enhanced Tools をダウンロードして展開する。

```bash
$ qemu-img create msdos.disk 1G
$ qemu-system-i386 -hda msdos.img -fda Disk1.img -boot a
```

![](img/msdos000.png)

"Enter" を押下

![](img/msdos001.png)

"Enter" を押下

![](img/msdos002.png)

"Enter" を押下

![](img/msdos003.png)

フォーマットが始まるので完了するまで待つ

![](img/msdos004.png)

"Enter" を押下

![](img/msdos005.png)

"Enter" を押下

![](img/msdos006.png)

![](img/msdos007.png)

"Ctrl + Option + 2" を押下して、qemu モニターコンソールに移動

![](img/msdos008.png)

以下を実行して、"Ctrl + Option + 1" で戻る
```
(qemu) change floppy0 Disk2.img
```

![](img/msdos009.png)

"Enter" を押下

![](img/msdos010.png)

"Ctrl + Option + 2" を押下して、qemu モニターコンソールに移動して、以下を実行
```
(qemu) change floppy0 Disk3.img
```

![](img/msdos011.png)

"Ctrl + Option + 1" で戻って、"Enter" を押下

![](img/msdos012.png)

"Ctrl + Option + 2" を押下して、qemu モニターコンソールに移動して、以下を実行
```
(qemu) eject floppy0
```

"Ctrl + Option + 1" で戻って、"Enter" を押下

![](img/msdos013.png)

"Enter" を押下

これでインストールが完了しているので、以降は以下で MS-DOS を起動させることができる。
```bash
$ qemu-system-i386 -hda msdos.img -boot c
```
### Links
- [Installing MS-DOS on Qemu - Computer History Wiki](https://gunkies.org/wiki/Installing_MS-DOS_on_Qemu)
- [WinWorld: MS-DOS 6.22](https://winworldpc.com/product/ms-dos/622)




## DEBUG
- `A [address]` (Assemble): アセンブリコードを入力する
- `D [address] [address]` (Dump): メモリの内容をダンプする
- `E address [list]` (Edit): メモリの内容を編集する
- `G[=address] [address]` (Go): プログラムを実行する
- `N` (Name): ファイル名を指定する
- `Q` (Quit): 終了する
- `R [register]` (Register): レジスタを表示もしくは設定する
- `T [address]`: 指定したメモリのプログラムを 1 命令実行し、全レジスタの内容と次に実行する命令を表示する
- `U [address] [address]` (Unassemble): 逆アセンブルを行う
- `W` (Write): メモリ内容をファイルに出力する
- `?` (Help): ヘルプ画面を表示する


### Links
- DOS DEBUG Commands
https://montcs.bloomu.edu/Information/LowLevel/DOS-Debug.html




## QEMU
### ハードディスクイメージの作成
```bash
$ qemu-img create -f raw <ファイル> <サイズ>
```


### 仮想マシンの起動
```bash
$ qemu-system-i386 <イメージファイル> <オプション>
```

- Options
  - `-boot a`
    - 起動デバイスにフロッピーディスクを指定する
  - `-boot c`
    - 起動デバイスにハードディスクを指定する (デフォルト)
  - `-boot d`
    - 起動デバイスに CD-ROM/DVD を指定する
  - `-fda/-fdb <ファイル>`
    - フロッピーディスク 0/1 となるファイルを指定する
  - `-hda/-hdb/-hdc/-hdd <ファイル>`
    - ハードディスク 0/1/2/3 となるファイルを指定する
  - `-cdrom <ファイル>`
    - CD-ROM/DVD となる iso イメージファイルを指定する



### Links
- [QEMU - ArchWiki](https://wiki.archlinux.jp/index.php/QEMU)




## MASM
FreeDOS および MS-DOS 上で動作する MASM の導入方法がわからなかったので、MASM 互換の JWasm を使う。

1. [ここ](http://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/distributions/1.2/repos/pkg-html/jwasm.html) から [jwasm.zip](http://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/repositories/latest/devel/jwasm.zip) をダウンロードする。
2. jwasm.zip を回答して、jwasm/DEVEL/JWASM を DOS に移動させる。
3. DOS を起動して、パスを通す。


```
JWASMR -bin -Fo <FILE>.COM <FILE>.ASM
```


### Links
- [ibiblio.org FreeDOS Package -- JWasm (Development)](http://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/distributions/1.2/repos/pkg-html/jwasm.html)
- [JWasm](https://www.japheth.de/JWasm.html)
- [JWasm Readme](https://www.japheth.de/JWasm/Readme.html)
- [JWasm Manual](https://www.japheth.de/JWasm/Manual.html)




## Mac で QEMU 環境にホストからファイルをコピーする
基本的には、イメージファイルを一旦物理ディスクとして認識させたあとに、適当なマウントポイントにマウントする形となる。

```bash
$ hdiutil attach -nomount <path to image file>
$ diskutil list
$ mount_msdos <device file> <mount point>
```
```bash
$ umount <mount point>
$ hdiutil detach <device name>
```
