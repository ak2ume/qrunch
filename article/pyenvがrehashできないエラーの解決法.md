# 更新ログ
- 2020/Aug/14 新規エントリ

# このエントリで言いたいこと
fishを起動時に発生するpyenvのrehashエラーを解決した。

# 環境
- MacBook Pro (13-inch, 2019, Four Thunderbolt 3 ports)
プロセッサ：2.4 GHz クアッドコアIntel Core i5
メモリ：16 GB 2133 MHz LPDDR3
- MacOS Catalina (10.15.6)
- pyenv 1.2.19

# 本論
## きっかけ
pyenvを導入したところ、ターミナル(fish)の起動時に下記エラーが表示されてとても煩わしかった。

``pyenv: cannot rehash: /Users/XXXX/.pyenv/shims isn't writable``

気が向いたときにsudoでrehashする運用で諦めていたんですが、
rbenvの同現象を解決している人をたまたま見つけたので、ためしにやってみました。

## ネタ2
[rbenvがrehash出来ないエラーを解決した話][rbenv]
と同じく、shimsの所有者がrootになっていた。
ので、
```
cd /Users/XXXX/.pyenv/
sudo chown XXXX ./shims/
```
で所有者を変更したところ、ターミナルを起動してもrehash時のエラーが発生しなくなった。

# まだ分からないこと
- なし

# reference
- [rbenvがrehash出来ないエラーを解決した話][rbenv]

[rbenv]: http://teinen.hatenablog.jp/entry/2018/04/12/114359
