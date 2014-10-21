# TinyOS開発環境

## 概要
- このレポジトリにはTinyOS開発用Linux環境を提供するためのVagrant関連ファイルが格納されています
- Vagrantを使用して半自動的に環境を構築できます

## 環境の概要
- OS
	- Debian GNU/Linux (jessie alpha1 release)
- ハードウェア関連
	- Architecture	- x86_64
	- Number of CPU cores	- 2
	- Memory	- 4096MB
- 導入済み主要ソフト
	- git (debian package)
	- 各種ビルドツール (debian package)
		- gcc, make等
	- gcc-avr (debian package)
	- avrdude (debian package)
	- java (debian package, openjdk-7)
	- emacs (debian package)
- ホストへのPort forwarding
	- SSH - guest:22 -> host:2222

## 環境構築手順
- `doc/setup.pdf`参照

## Copyright, License
- Copyright (c) 2014, Shigemi ISHIDA
- This software is released under the BSD 3-clause license: See `LICENSE`.