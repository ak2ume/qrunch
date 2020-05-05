# 更新ログ
- 2020/May./05 HIEの導入について追記
- 2020/May./05 新規エントリ

# このエントリで言いたいこと
MacにHaskellの開発環境を構築してみたので、その手順を残しておきます。

# 環境
- MacBook Pro (13-inch, 2019, Four Thunderbolt 3 ports)
プロセッサ：2.4 GHz クアッドコアIntel Core i5
メモリ：16 GB 2133 MHz LPDDR3
- MacOS Catalina (10.15.4)

# 本論
## stackをインストール
Homebrewでインストール
```
brew install stack
```
2020/May./5時点でのバージョンは2.1.3 (x86_64)

stackを使ってコンパイラ(GHC)や基本パッケージをインストール
```
stack setup
```
ダウンロード含めて2.4分くらいかかった。
※余談ですが、fishで実行時間が表示されるの便利。

## プロジェクト作成
```
stack new helloworld
```
defaultのプロジェクトファイル一式が生成される。

## ビルド&実行
src/Lib.hsの中身(defaultは"someFunc"の文字列を出力する処理)を書き換える。
```
someFunc = putStrLn "Hello, world."
```
ビルド
```
stack build
```
stackを実行するたびに現状は以下のwarning(?)が表示される。
とりあえず無視。
> Stack has not been tested with GHC versions above 8.6, and using 8.8.3, this may fail
> Stack has not been tested with Cabal versions above 2.4, but version 3.0.1.0 was found, this may fail

実行
```
stack exec helloworld-exe
```
ちゃんと表示した。Quite Easily Done!!

> Hello, world.

## 便利機能を追加(未完)
VS CodeでHaskell Language Serverを使うため、
haskell ide engineをインストール
```
git clone https://github.com/haskell/haskell-ide-engine --recursive
cd haskell-ide-engine
./install.hs hie
```
、、、が最後のインストールコマンドで14分近くかかった挙句、ConnectionFalilureで失敗した。

> HttpExceptionRequest Request {
>   host                 = "s3.amazonaws.com"
>   port                 = 443
>   secure               = True
>   requestHeaders       = [("User-Agent","Haskell pantry package")]
>   path                 = "/hackage.fpcomplete.com/package/unsafe-0.0.tar.gz"
>   queryString          = ""
>   method               = "GET"
>   proxy                = Nothing
>   rawBody              = False
>   redirectCount        = 10
>   responseTimeout      = ResponseTimeoutDefault
>   requestVersion       = HTTP/1.1
> }
>  (ConnectionFailure Network.Socket.getAddrInfo (called with preferred socket type/protocol: AddrInfo {addrFlags = [AI_ADDRCONFIG], addrFamily = AF_UNSPEC, addrSocketType = Stream, addrProtocol = 6, addrAddress = <assumed to be undefined>, addrCanonName = <assumed to be undefined>}, host name: Just "s3.amazonaws.com", service name: Just "443"): does not exist (nodename nor servname provided, or not known))
> Progress 163/228

Amazon S3 サービスが見つからない?
後日retryする。
(2020/May/05 追記)
VS CodeでHaskell Language ServerをDisableにしたり、インストール中にMacを触らないようにしたりして、何回かretryしたら通った。
何が決め手だったか不明だが、とりあえず先には進めたのでよし!!

# まだ分からないこと
- stack実行時に表示されるwarningを消したい。stackが古い?
- AtCoderではLib.hsを提出するだけで行ける?エントリポイントを書かないといけなさそう。

# reference
- [【2019版】 Mac に Haskell の環境構築をして stack で helloworld するまで][qiita]
- [MacでHaskellの環境を構築する][noozui]
- [vscodeでのhaskell開発環境作成][ngiy]

[noozui]: https://www.nooozui.com/entry/20191111/1573473976
[ngiy]: https://ngiy.hatenablog.com/entry/2018/06/06/142147
[qiita]: https://qiita.com/yusk_1860/items/deeb025953990ac09dce
