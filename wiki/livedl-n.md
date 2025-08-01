# livedl-n  

livedl-nは2025年5月31日をもって開発終了いたしました  
現時点(2025/7/20)ではコメントのみダウンロード可能ですが、今後のニコ生の仕様変更には対応いたしません  
[https://github.com/nnn-revo2012/livedl-n](https://github.com/nnn-revo2012/livedl-n) は公開終了いたしました(2025年8月1日)  
本Wikiは一応残しておきます  

私にはよくわかりませんが、[四八福星間開発](https://person-of-ehomaki.blog.jp) というサイトを見るといいかもしれません  

## 動画のダウンロードについて  
**ニコニコ生放送（ニコ生）は2025/02/05から新動画サーバー(dlive)の配信に移行しています。  
dliveで配信する動画はすべてAES128暗号化されており、これを解除する方法の公開やツール作成は日本の著作権法に違反する可能性があります。  
現在の作者(nnn-revo2012)は日本在住なのでこのツールを対応させることができません。  
※アメリカ、EU、中国、韓国を含むほとんどの国でもDRM暗号化の解除は違法なのでAES暗号化動画の解除も違法になる可能性があります。  
今後の動画についてはご自分で情報を探すなりして対応してください。**  

## はじめに
このページでは、livedl-n(以下livedl)の使い方について説明します。  
本ツールはhimananiitoさんが作成されたlivedlを元にしてnnn-revo2012がニコ生の仕様変更対応、機能追加を行ったツールです。  

## ダウンロード
本ソフトウェアの公開は終了いたしました(2025年8月1日)  

## 使い方(概要)  
コマンドライン（PowerShellやコマンドプロンプト,シェル等）で実行して下さい。  
ただし、PowerShellの場合は基本的には livedl は ./livedl と読み替えて下さい。  
- 起動時に放送URLがオプションに渡された場合はそのまま録画を開始します。  
- 放送URL及び各オプションは半角スペースで区切って下さい。  

コマンドラインで以下のように実行します。  

```
livedl [COMMAND] options... [--] FILE
```

### コマンド/COMMAND  
以下のいずれかを指定。ただし、FILEでURLを入力してサイトが判定できる場合には指定不要。  

|COMMAND|説明|
|:---|:---|
|-nico|ニコニコ生放送の録画|
|-tcas|ツイキャスの録画|
|-d2m|録画済みのデータベース(sqlite3)を動画ファイル(mp4/ts)に変換する|
|-dbinfo|録画済みのdb(.sqlite3)の各種情報を表示する  e.g. ```livedl -dbinfo -- 'C:/home/hogehoge/livedl/rec/lvxxxxxxxx.sqlite3'```|
|-d2h|[実験的] 録画済みのdb(.sqlite3)を視聴するためのHLSサーバを立てる(-db-to-hls)  開始シーケンス番号は（変換ではないが） -nico-conv-seqno-start で指定  使用例：```livedl lvXXXXXXXXX.sqlite3 -d2h -nico-hls-port 12345 -nico-conv-seqno-start 2780```|

### オプション/option  

|OPTION|説明|
|:---|:---|
|-h|ヘルプを表示|
|-v|バージョンを表示|
|-no-chdir|起動する時chdirしない(conf.dbは起動したディレクトリに作成されます)|
|--|後にオプションが無いことを指定|

その他のオプションは各サイトオプションの場合の説明を見て下さい。  

### ファイル/FILE  
録画したいURL、固有のID（いずれかの録画コマンド）またはファイル名（ローカルファイル操作コマンド）を指定します。  

### プログラムの終了方法  
録画中に終了する場合は、正しく終了するためにコンソールの画面上でCtrl-Cを入力して終了して下さい。  
プログラムを突然終了した場合にZIP/データベース ファイルの最終処理ができません。  

### 設定ファイルについて(備考)  
設定はログイン情報設定ファイル(account.db)と一般オプション設定ファイル(conf.db)の２つに保存されます  

ログイン情報設定ファイルには、サイト(ニコニコ)のログイン情報が保持されます。  
ログイン情報設定ファイルの場所は以下の優先度が最も高いものとなります。  

- 環境変数 LIVEDL_DIR がある場合、$LIVEDL_DIR 直下の account.db  
- 環境変数 APPDATA がある場合、$APPDATA/livedl/account.db  
- 環境変数 HOME がある場合、$HOME/.livedl/account.db  
- Windowsでのデフォルトは、%APPDATA%\livedl\account.db です。  

ログイン関連で問題が出た場合は本ファイルを削除してみて下さい。  

一般オプション設定ファイルには、コマンドのオプション(ファイル名フォーマット)など、アカウント情報以外が保持されます。  
一般オプション設定ファイルの場所は実行ファイルと同じディレクトリの conf.db です。  

設定関連で問題が出た場合は本ファイルを削除してみて下さい。  

## オプション（ニコニコ生放送）  

|オプション 　　　　　　　　　　　　　　|設定保持|説明|
|:---|:---:|:---|
|-nico-login id,password|〇|ニコニコのIDとパスワードを設定し設定ファイルに書き込む **2段階認証(MFA)に対応しています**|
|-nico-cookies firefox| |firefoxのcookieを使用する(デフォルトはdefault-release) profileまたはcookiefileを直接指定も可能 スペースが入る場合はquoteで囲む 下記別表参照|
|-nico-session <session>| |Cookie[user_session]を指定する|
|-nico-hls-port portnum| |[実験的] ローカルなHLSサーバのポート番号。指定時に、指定のポート番号にHLSのサーバーを立てる。ffplay(確認済)やVLC(未確認)等にて、http://127.0.0.1:<指定したポート番号> にアクセスすることで映像を確認することができる。接続時に時間がかかることがあるので、localhostではなく127.0.0.1とすることを推奨。|
|-nico-limit-bw num|〇|新配信におけるプレイリストのBANDWIDTHの上限値を設定する。設定値を下回るプレイリストがない場合、最も小さいものを使用する。0 = 制限なし(デフォルト) audio_high or audio_only = 音声のみ|
|-nico-exec-bw "FORMAT"|〇|実行ファイル起動時に画質を指定する 具体的にどう設定するかは使うツール側のHELPやマニュアルを参照ください -nico-limit-bwとは連動していません|
|-nico-fast-ts| |新配信での倍速タイムシフト録画を有効にする|
|-nico-fast-ts=(on/off)|〇|上記設定を保持する|
|-nico-format "FORMAT"|〇|新配信における保存時のファイル名を指定する。デフォルトは "?PID?-?UNAME?-?TITLE?" 。例えば、recというフォルダの下に、ユーザ名でフォルダを分けたい場合は "rec/?UNAME?/?PID?-?UNAME?-?TITLE?" のようにする。拡張子をここで指定しないこと。FORMATについては下記別表参照。|
|-nico-auto-convert=on|〇|録画終了後自動的に動画ファイルに変換するように設定|
|-nico-auto-convert=off|〇|上記を無効に設定|
|-nico-auto-delete-mode 0|〇|自動変換後にデータベースファイルを削除しないように設定（デフォルト）|
|-nico-auto-delete-mode 1|〇|自動変換で動画ファイルが分割されなかった場合のみ削除するように設定|
|-nico-auto-delete-mode 2|〇|自動変換で動画ファイルが分割されても削除するように設定|
|-nico-login-only=on|〇|必ずログイン状態で録画する|
|-nico-login-only=off|〇|非ログインでも録画可能とする(デフォルト)|
|-nico-force-reservation=on|〇|視聴にタイムシフト予約が必要な場合に自動的に上書きする|
|-nico-force-reservation=off|〇|自動的にタイムシフト予約しない(デフォルト)変換オプション（-nico-auto-convert=on または -d2m の変換時）|
|-nico-skip-hb=on|〇|コメント書き出し時に/hbコマンドを出さない|
|-nico-skip-hb=off|〇|コメント書き出し時に/hbコマンドも出す(デフォルト)|
|-nico-ts-start <num>| |タイムシフトの録画を指定した再生時間（秒）から開始する|
|-nico-ts-stop <num>| |タイムシフトの録画を指定した再生時間（秒）で停止する|
| | |上記2つは ＜分＞:＜秒＞ または ＜時＞:＜分＞:＜秒＞ の形式でも指定可能|
|-nico-ts-start-min <num>| |タイムシフトの録画を指定した再生時間（分）から開始する|
|-nico-ts-stop-min <num>| |タイムシフトの録画を指定した再生時間（分）で停止する|
| | |上記2つは ＜時＞:＜分＞ の形式でも指定可能|
|-nico-no-streamlink=on|〇|Streamlinkを使用しない(デフォルト)|
|-nico-no-streamlink=off|〇|Streamlinkを使用する|
|-nico-no-ytdlp=on|〇|yt-dlpを使用しない(デフォルト)|
|-nico-no-ytdlp=off|〇|yt-dlpを使用する|
|-nico-comment-only=on|〇|コメントのみダウンロードする|
|-nico-comment-only=off|〇|動画とコメントをダウンロードする(デフォルト)|
|変換オプション| | |
|-nico-conv-seqno-start <num>| |MP4への変換を指定したセグメント番号から開始する|
|-nico-conv-seqno-end <num>| |MP4への変換を指定したセグメント番号で終了する|
|-nico-conv-force-concat| |MP4への変換で画質変更または抜けがあっても分割しないように設定|
|-nico-conv-force-concat=on|〇|上記を有効に設定|
|-nico-conv-force-concat=off|〇|上記を無効に設定(デフォルト)|
|-nico-adjust-vpos=on|〇|コメント書き出し時にvposの値を補正する(デフォルト) vposの値が-1000より小さい場合はコメント出力しない|
|-nico-adjust-vpos=off|〇|コメント書き出し時にvposの値をそのまま出力する|
|-extract-chunks=off|〇|-d2mで動画ファイルに書き出す(デフォルト)|
|-extract-chunks=on|〇|-d2mで各々のチャンクを書き出す|
|-conv-ext=mp4|〇|変換時の出力の拡張子を.mp4とする(デフォルト)|
|-conv-ext=ts|〇|変換時の出力の拡張子を.tsとする|
|HTTP関連| | |
|-http-skip-verify=on|〇|TLS証明書の認証をスキップする (32bit版対策)|
|-http-skip-verify=off|〇|TLS証明書の認証をスキップしない (デフォルト)|
|-http-timeout <num>|〇|タイムアウト時間（秒）デフォルト: 30秒（最低値）|

### FORMATで指定可能な変数一覧  

|変数|説明|
|:---|:---|
|?PID?|ProgramId。lv1234567のような文字列。
|?UNAME?|ユーザ名。公式の場合、"official"
|?UID?|ユーザID。nicovideo.jp/user/に続く数字の列。公式の場合、"official"
|?CNAME?|チャンネル名。公式の場合、"official"
|?CID?|チャンネルID。co1234のような文字列。公式の場合、"official"
|?TITLE?|放送タイトル。
|?YEAR?|年4桁。開場ではなく開演時刻。以下同じ
|?MONTH?|月2桁
|?DAY?|日2桁
|?DAY8?|年4桁,月2桁,日2桁: "20180901"
|?DAY6?|年2桁,月2桁,日2桁: "180901"
|?HOUR?|時2桁
|?MINUTE?|分2桁
|?SECOND?|秒2桁
|?TIME6?|時2桁,分2桁,秒2桁
|?TIME4?|時2桁,分2桁

### 画質一覧  

|画質　　|-nico-limit-bw|
|:---|:--- |
|8Mbps 1080p60fps|14400000|
|6Mbps 1080p30fps|10800000|
|4Mbps 720p60fps|7200000|
|super_high(3Mbps)|5400000|
|high(2Mbps)|3600000|
|normal(1Mbps)|1800000|
|low(384Kbps)|691200|
|super_low(192Kbps)|345600|
|音声のみ|audio_high|
|音声のみ|audio_low|

### Firefoxのcookieを使用する  
```-nico-cookies firefox[:profile|cookiefile]``` 

- profile default-release のcookieを取得  
```
livedl -nico-cookies firefox
```  

- profile NicoTaro のcookieを取得  
```
livedl -nico-cookies firefox:NicoTaro
```  

- 直接cookiefileを指定  
```
livedl -nico-cookies firefox:'C:/Users/*******/AppData/Roaming/Mozilla/Firefox/Profiles/*****/cookies.sqlite'
``` 

**※Mac/Linuxで cookies from browser failed: firefox profiles not foundが 表示される場合は報告おねがいします**  
**※直接cookiefile指定の場合は必ず'か"で囲ってください**  
**※プロファイルにspaceを含む場合は'か"で囲ってください**  

## 初めて実行する場合（ニコニコ生放送のアカウント設定）  
ニコニコ生放送は、ほとんどの場合ログインが必要になるので```-nico-login id,password``` オプションにてニコニコのIDとパスワードを設定して下さい。  
（ログイン不要の番組の録画やfirefoxのcookieを利用する場合はこのオプションは不要）  
IDとパスワード、及びクッキー（セッション）は設定ファイルに保存されるため、1度-nico-loginを指定した後は、指定不要です。  

例（コマンドプロンプト）：  
```
livedl -nico-login "test@example.com,password" lv333333333
```  

例（Powershell、bash(sh)）：  
**必ずシングルクオーテーションで囲ってください**  
```
./livedl -nico-login 'test@example.com,password' lv333333333
```  

2回目以降（ニコニコ生放送） 
アカウント情報の指定は不要です。  

```
livedl lv333333333
```  

## 実行ファイルを起動する  
- **livedl を起動して動画を取得するために実行ファイル(yt-dlp/Streamlink)を起動する機能です**  
- **この機能が実際に必要になった際は著作権の関係で詳細や質問には答えられないと思います(これは2025/1/28に書いてます)**  
- livedlのユーザー情報(user_session)、ファイル名、proxy、画質、ＴＳの開始時間、終了時間を実行ファイルに引き継ぎます  
- **yt-dlpではＴＳの開始時間、終了時間を指定できません(yt-dlpにその機能がない)**  
- ~~現状では画質は最高のみとなります~~  
- **コメントはlivedlで取得します**  
  リアルタイム録画での動画とコメントの開始時間は同期不可能なので数秒ずれる可能性があります  
- この機能ではlivedl起動時にはsqlite3ファイルがありますが、**終了後設定に関わらず即時コメントを展開しsqlite3ファイルを削除します**  

### 手順
1. yt-dlpかStreamlinkを普通にインストールする(特にlivedlのあるフォルダの下にある必要はないです)  
  **必ずPATHを通しておいてください**  
  **すでに上記のいずれかがインストールしてありPATHを通してる状態では手順1.は不要です**  
2. **livedlを起動する際に以下のオプションをつけてください**  
  - yt-dlpを使う場合  
```
livedl -nico-no-ytdlp=off -nico-no-streamlink=on [その他のオプション] lvxxxxxxxxx
```  
  - Streamlinkを使う場合  
```
livedl -nico-no-ytdlp=on -nico-no-streamlink=off [その他のオプション] lvxxxxxxxxx
```  
3. livedl(およびyt-dlp/Streamlink)終了後、動画とコメントが出力されてると思います  
4. 次回以降起動する場合は``-nico-no-ytdlp=on|off -nico-no-streamlink=on/off``は指定しなくてもいいです  
