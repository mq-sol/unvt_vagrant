# UNVT のための Vagrantファイル

UNVTの開発で必要なものを包含したVagrantファイルです。


## 前提条件


## 開発環境

* VirtualBox
* Vagrant

をインストールしてください。

参考：
  [Qiita記事(windows版)](https://qiita.com/aoi70/items/b66a451f4b7f5f05beec)
  [Qiita記事(mac版)](https://qiita.com/uhooi/items/fed061205a13bdaaa514)


## Vagrantファイルの取得と実行

```bash
git clone https://github.com/mq-sol/unvt_vagrant

cd unvt_vagrant
vagrant up
```

VMの作成には時間がかかります。

### sshでログイン

作成後、VMにSSHで接続してWordpressのセットアップのスクリプトを実行します。
Windowsならコマンドプロンプトなどターミナルソフトを起動してください。

ターミナル上で下記のコマンドを実行します。

```bash
vagrant ssh
```

### terminalソフト(Teratermなど)でのログイン方法

ログインできるIPは２つあります。

ssh vagrant@localhost:2222

| 項目 | 値 |
| -- | -- |
| アカウント | vagrant |
| パスワード | vagrant |
| ポート番号 | 2222 |
| ホスト名 | localhost |

ssh vagrant@192.168.56.50

| 項目 | 値 |
| -- | -- |
| アカウント | vagrant |
| パスワード | vagrant |
| ポート番号 | 22 |
| ホスト名 | 192.168.56.50 |

でログインできます。

---

## Vagrantの使い方

※ VMの起動・終了はVirtualboxアプリの操作で行わないでください。

* Vagrantの起動(初めてVMを作成も含む)

```bash
vagrant up
```

* Vagrantの停止

```bash
vagrant halt
```

* VagrantのVMの削除（Vagrantファイルを更新した際に実行します）

```bash
vagrant destroy
```

---

## メモリーのサイズの変更

```ruby
vb.memory = "2048"
```
の値を増やしてください。

## ファイルのやり取り

Vagrant ファイルを置いているフォルダーは VM上の `/vagrant`ディレクトリにマウントされます。
このフォルダにLASファイルを置いてからVMの実体にコピーするといいでしょう。

```bash
cp /vagrant/*.las ~
```
