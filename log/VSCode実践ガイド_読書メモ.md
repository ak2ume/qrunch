# 更新ログ
- 2020/Mar./22 新規エントリ (3章まで)
- 2020/Mar./28 新規エントリ (5章まで)
- 2020/Apr./04 新規エントリ (6章まで)

# 環境
- 書籍：[Visual Studio Code実践ガイド 最新コードエディタを使い倒すテクニック][book]

# 作業メモ
- __done__ 1章　インストールと初期設定 
  - codeコマンド：引数として渡したフォルダーをVSCodeのワークスペースとして開くことができる。
- __done__ 2章　画面構成と基本機能
  - Cmd+Shift+¥ : 対応する括弧にカーソルを移動する。
  - Cmd+l : 行を選択する。
  - Cmd+Ctrl+Shift+→← : 囲みを選択する。さらに外/内側の範囲に拡張/縮小する。
  - Cmd+/ : ラインコメントを設定 or 削除する。
  - Cmd+Ctrl+[/] : ブロック折り畳む or 展開する。
  - Cmd+T : すべてのファイルのシンボルをあいまい検索する。
  - Cmd+F12 : 実装へ移動する。
  - Ctrl+- : 前のファイルへ戻る。
  - Ctrl+Shift+- : 戻るをundoする。
  - Ctrl+Spaceでインテリセンス中の上下移動はCtrl+N/Ctrl+P、Tab/Enterで確定する。
  - Cmd+Shift+l : 選択中の語句でマルチカーソル開始する。
  - Opt(Alt)を押しながらクリックでマルチカーソル追加する。
  - Opt(Alt)+Shift+ドラッグ : 矩形選択する。
- __done__ 3章　ビューとコマンドパレット
  - エクスプローラビュー上で未保存のファイルの右クリックメニューから「保存済みと比較」できる。
- __done__ 4章　Gitとの連携
  - GitLensとGit History
- __done__ 5章　デバッグ機能
  - デバッグアダプタプロトコル(DAP)に従うデバッグアダプタによってデバッグ機能を利用できる
    - [74thさんによるデバッガ実装状況まとめ][debugger_implement_status]
    - [森下篤著『VisualStudioCodeデバッグ技術』][book_debug]
  - F11はMission Controlでデスクトップ表示に割り当てていたのでstep inできない。
    →システム環境設定でMission Controlの機能を切った。
  - breakpoint
    - 通常breakpoint : F9 or 行番号左をクリック
    - inline breakpoint : 複数処理行内の設定したい場所でShift+F9
    - 条件付きbreakpoint : 右クリックメニュー
      - EXPRESSON : if文の中身を記述
  - WATCH
    - 任意の評価式を入力できる。
  - DEBUG CONSOLE
    - 評価式で変数を確認したり、関数を実行したりできる。
    - 指定行でログの出力を行える。→print文デバッグしなくていい!!
      - 行番号左側を右クリックして「add logpoint」
  - launch.json
    - "name" : デバッグビューに表示される設定名
    - "type" : 拡張機能が指定する名称。READMEやテンプレート、スニペットから流用する。
    - "request" : "launch"(プログラム起動) or "attach"(既存プロセスにアタッチ)
    - "program" : ランタイムプログラムで実行するソースコード
    - "args" : "program"実行時の引数
    - "env" : 実行時の環境変数
- __done__ 6章　そのほかの機能
  - タスクランナー
    - ビルド処理の依存解決や複数のツール実行とりまとめ
    - VSCodeのタスク機能では成果物の管理や実行条件の設定を行えない
    - "Task: Run Task" で自動認識したタスク一覧から選択して実行
    - "Tasks: Configure Task" で自動認識したタスクをもとに設定編集
      - 設定項目の詳細は第2部も参照
  - リント
    - エラー箇所にカーソルがある状態でマウスをあてるとクイックフィックスで修正候補を選択できる。
    - タスクランナーでリント機能を記述すればパラメータ指定などを行える。
    - problemMatcherは正規表現で記述する
  - スニペット
    - "@category:snippets"を拡張機能ビューで検索すれば見つかる
    - スニペット内のプレースホルダはtabで移動
    - 自作する場合、"Preferences: Configure User Snippets"
      - プレースホルダは`$1`もしくは`${2:default}`と記載
      - |で囲った,区切りは選択式になる
      - カーソル移動位置は`$0`
      - 変数を正規表現で置換することも可能
  - ターミナル
- __skip__ 7章　リモート開発機能
- __here__ 8章　カスタマイズ
  - 

# まだ分からないこと
- なし

# reference
- [Visual Studio Code実践ガイド 最新コードエディタを使い倒すテクニック][book]
- [74thさんによるデバッガ実装状況まとめ][debugger_implement_status]
- [森下篤著『VisualStudioCodeデバッグ技術』][book_debug]

[book]: https://www.amazon.co.jp/Visual-Studio-Code%E5%AE%9F%E8%B7%B5%E3%82%AC%E3%82%A4%E3%83%89-%E2%80%94%E2%80%94-%E6%9C%80%E6%96%B0%E3%82%B3%E3%83%BC%E3%83%89%E3%82%A8%E3%83%87%E3%82%A3%E3%82%BF%E3%82%92%E4%BD%BF%E3%81%84%E5%80%92%E3%81%99%E3%83%86%E3%82%AF%E3%83%8B%E3%83%83%E3%82%AF-ebook/dp/B084SS63L4/ref=pd_rhf_gw_p_img_2?_encoding=UTF8&psc=1&refRID=6P5JAMF7DD64GKZ2C35B
[debugger_implement_status]: https://74th.github.io/vscode-debug-specs/
[book_debug]: https://www.amazon.co.jp/Visual-Studio-Code%E3%83%87%E3%83%90%E3%83%83%E3%82%B0%E6%8A%80%E8%A1%93-%E6%8A%80%E8%A1%93%E3%81%AE%E6%B3%89%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA%EF%BC%88NextPublishing%EF%BC%89-%E6%A3%AE%E4%B8%8B-ebook/dp/B07KXGNVS2/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=
