# 更新ログ
- 2020/May./03 新規エントリ

# このエントリで言いたいこと
Macにfish(the friendly interactive shell)環境を整えてみたので、手順を残しておきます。

# 環境
- MacBook Pro (13-inch, 2019, Four Thunderbolt 3 ports)
プロセッサ：2.4 GHz クアッドコアIntel Core i5
メモリ：16 GB 2133 MHz LPDDR3
- MacOS Catalina (10.15.4)
- iTerm2 Build 3.3.9

# 本論
## きっかけ
ちょうどtwitter上でfishに関するtweetが流れてきて、
そのタイミングで技術書典 応援祭にて[fishのすゝめ][gijutsushoten] (リンク先はBOOTH)という書籍を見つけたり、
縁を感じたのでfish環境構築してみようと思いました。
なお、普段はzshですがほとんど使いこなせていません。
ま、遊びのひとつってことで。。。

## インストール
Qiita記事([bash 使いが fish でスイスイ泳げるようになるまで (in Mac)][Qiita])も参考に。
まずは本体をhomebrewでインストール。
```
brew install fish
```
2020/May./03時点でのバージョンは3.1.2でした。

## 設定
which fishした結果を `/etc/shells` に追記する。
ログインシェルにはしない。([fishのすゝめ][gijutsushoten]より)
かわりに、`.zshrc` の最後でfishを起動する処理を追加した。
まずここまででiTerm2を再起動し、fishが立ち上がることを確認。

## プラグイン追加

### Fisher (プラグイン管理)
```
curl https://git.io/fisher --create-dirs -sLo ~/.config/fish/functions/fisher.fish
```

### bobthefish (git branchをプロンプトに表示)
```
fisher add oh-my-fish/theme-bobthefish
```
入れた途端プロンプト表記が変わった。
合わせてPowerline fontsをインストールする。
```
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
./install.sh
cd ..
rm -rf fonts
```
iTerm2のPreferenceにて、
Profilesに新たなProfileを追加し、FontをSource Code Pro for Powe...に設定する。
ちょっと文字表示が小さくなるのでSizeを14に変更。
Other Actions... で set as a defaultを選ぶ。
Profile Name欄の★が移動したらOK。
ただ、branch名が表示されないので、
`~/.config/fish/config.fish` を作成して以下を記載。
```
set -g theme_display_git_master_branch yes
```
再読み込みしたら表示されるようになった!!

### plugin-peco (インクリメンタルサーチ)
まずはhomebrewでpecoをインストール
```
brew install peco
```
Fisherでfishプラグインをインストール
```
fisher add plugin-peco
```
`~/.config/fish/config.fish` に Ctrl+r へのキーバインド設定を追記
```
function fish_user_key_bindings
    bind \cr peco_select_history # Bind for prco history to Ctrl+r
end
```

### z (履歴からディレクトリ移動)
```
fisher add jethrokuan/z
```

### ghq (gitリポジトリ管理)
まずはhomebrewでghqをインストール
```
brew install ghq
```
Fisherでfishプラグインをインストール
```
fisher add decors/fish-ghq
```
`~/.config/fish/config.fish` に インクリメンタルサーチにpecoを使う設定を追記
```
set GHQ_SELECTOR peco
```
これを機に、GHQでリポジトリ管理するようにします。

# まだ分からないこと
- なし

# reference
- [bash 使いが fish でスイスイ泳げるようになるまで (in Mac)][Qiita]
- [fishのすゝめ][gijutsushoten]

[Qiita]: https://qiita.com/daichildren98/items/988278c9dc11b92867b5
[gijutsushoten]: https://ik-fib.booth.pm/items/1887001

