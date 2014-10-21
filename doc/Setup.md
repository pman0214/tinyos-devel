# TinyOS開発環境のセットアップ

## はじめに

- このドキュメントは，[TinyOS](http://www.tinyos.net/)向けの開発環境を構築する手順を示したものである．
- 本レポジトリに含まれている`Vagrantfile`を使用して仮想Linuxマシンを半自動的に構築し，TinyOS開発環境を整備する．
- 開発対象としてAVR搭載のMOTE（MICAz等）を想定してツールをインストールしている．

## 環境構築

- まずは仮想マシン上に開発環境を構築する．
- 構築手順の概要は以下の通りである．
	1. VagrantとVirtualBoxの導入
	1. Vagrant omnibus pluginの導入
	1. レポジトリのclone
	1. 仮想マシンの起動と設定

### VagrantとVirtualBoxの導入
- Vagrantは仮想マシンを半自動的に作成するツールである．
- 以下から取得し，手順に従ってインストールしておく．
	- <http://www.vagrantup.com/>

- VirtualBoxはx86仮想化ソフトウェアである．
- 以下から取得し，手順に従ってインストールしておく．
	- <https://www.virtualbox.org/>
	- 執筆時点の最新版（4.3.18）でも修正されていないバグがあるため，ver 4.3.6をインストールする．
		- OpenGL周りのバグ[#12746](https://www.virtualbox.org/ticket/12746)，[#12941](https://www.virtualbox.org/ticket/12941)．

### Vagrant pluginの導入

- Macユーザは「ターミナル.app」を，Windowsユーザは「コマンドプロンプト」を開き，以下のコマンドを実行する．
	- 「ターミナル.app」はSpotlightに`Terminal`と入力すれば起動できる．
	- 「コマンドプロンプト」は`Windows+R`を押して`cmd`と入力すれば起動できる．

```
$ vagrant plugin install vagrant-omnibus
$ vagrant plugin install vagrant-proxyconf
```

- OSXでエラーが出る場合には先頭に`NOKOGIRI_USE_SYSTEM_LIBRARIES=1 `を付けて試してみる．


### レポジトリのclone
- Windowsユーザは`git`をインストールしておく．
- gitを使って以下のレポジトリをcloneし，submoduleを入手する．

```
$ git clone https://github.com/pman0214/tinyos-devel.git
$ cd tinyos-devel
$ git submodule init
$ git submodule update
```

### 仮想マシンの起動と設定

- 仮想マシンを起動する．
	- 時間はかかるが，以下のコマンドを入力すれば仮想マシンが起動して各種アプリケーションが自動的にインストール・設定される．

```
vagrant up
```

- アプリケーションのダウンロード先が混雑している場合など，上記コマンドがエラー終了する場合がある．その場合には以下のコマンドをエラー無く終了するまで繰り返し実行する．

```
$ vagrant provision
```

- エラー無く終了したら，以下のコマンドで仮想マシンを停止する．

```
$ vagrant halt
```
