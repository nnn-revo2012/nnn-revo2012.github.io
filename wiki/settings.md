# ニコ生向けSlNicoLiveRec(Streamlink)の設定、FAQ  

## 目次  

- [SlNicoLiveRec(Streamlink --default-stream)で指定する画質設定一覧](https://nnn-revo2012.github.io/wiki/settings#slnicoliverecstreamlink-default-stream%E3%81%A7%E6%8C%87%E5%AE%9A%E3%81%99%E3%82%8B%E7%94%BB%E8%B3%AA%E8%A8%AD%E5%AE%9A%E4%B8%80%E8%A6%A7)  
  - [ユーザー生放送、チャンネル、公式全て録画する](https://nnn-revo2012.github.io/wiki/settings#%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E7%94%9F%E6%94%BE%E9%80%81%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E5%85%AC%E5%BC%8F%E5%85%A8%E3%81%A6%E9%8C%B2%E7%94%BB%E3%81%99%E3%82%8B)  
  - [チャンネル、公式のみ録画する](https://nnn-revo2012.github.io/wiki/settings#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E5%85%AC%E5%BC%8F%E3%81%AE%E3%81%BF%E9%8C%B2%E7%94%BB%E3%81%99%E3%82%8B)  

- [SlNicoLiveRecで「E-Mail、Password でログインしました」と表示されるが何もしないで終了する](https://nnn-revo2012.github.io/wiki/settings#slnicoliverec%E3%81%A7e-mailpassword-%E3%81%A7%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%97%E3%81%BE%E3%81%97%E3%81%9F%E3%81%A8%E8%A1%A8%E7%A4%BA%E3%81%95%E3%82%8C%E3%82%8B%E3%81%8C%E4%BD%95%E3%82%82%E3%81%97%E3%81%AA%E3%81%84%E3%81%A7%E7%B5%82%E4%BA%86%E3%81%99%E3%82%8B)  

- [SlNicoLiveRecで「user_sessionでログイン」に設定する方法](https://nnn-revo2012.github.io/wiki/settings#slnicoliverec%E3%81%A7user_session%E3%81%A7%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AB%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95)  
  - [☆Chromeの場合](https://nnn-revo2012.github.io/wiki/settings#chrome%E3%81%AE%E5%A0%B4%E5%90%88)  
  - [☆Firefoxの場合](https://nnn-revo2012.github.io/wiki/settings#firefox%E3%81%AE%E5%A0%B4%E5%90%88)  
    - [■NicoGetCookieを使う（おすすめ）](https://nnn-revo2012.github.io/wiki/settings#nicogetcookie%E3%82%92%E4%BD%BF%E3%81%86%E3%81%8A%E3%81%99%E3%81%99%E3%82%81)  
    - [■直接FirefoxのCookieを取得する](https://nnn-revo2012.github.io/wiki/settings#%E7%9B%B4%E6%8E%A5firefox%E3%81%AEcookie%E3%82%92%E5%8F%96%E5%BE%97%E3%81%99%E3%82%8B)  
<p>

- [SlNicoLiveRec(Streamlink)で「配信していません」が表示され録画できない](https://nnn-revo2012.github.io/wiki/settings#slnicoliverecstreamlink%E3%81%A7%E9%85%8D%E4%BF%A1%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%9B%E3%82%93%E3%81%8C%E8%A1%A8%E7%A4%BA%E3%81%95%E3%82%8C%E9%8C%B2%E7%94%BB%E3%81%A7%E3%81%8D%E3%81%AA%E3%81%84)  

***
## SlNicoLiveRec(Streamlink --default-stream)で指定する画質設定一覧  

コピペするように"＊＊＊＊"のように囲ってあります  
 ~~＊SlNicoLiveRecの場合は、録画画質→default-streamにコピペした後両端の""を削除してください~~  

**ユーザー生のタイムシフトは2026年3月29日まで新旧仕様の画質が混在する**  
**（2026年1月27日までのユーザー生のタイムシフトは旧画質、1月28日以降のタイムシフトは新画質になる）**  

### ユーザー生放送、チャンネル、公式全て録画する  

最高8Mbps（最高6Mbpsの場合も同じ）  

何も指定しない  
または  
```
--default-stream best
```
または  
```
"1080p,1920p,720p,1280p,480p,854p,450p,800p,450p_alt,800p_alt,288p,512p,288p_alt,512p_alt"
```

最高3Mbps（最高4Mbpsの場合も同じ）
```
"720p,1280p,480p,854p,450p,800p,450p_alt,800p_alt,288p,512p,288p_alt,512p_alt"
```

最高2Mbps/1.5Mbps
```
"480p,854p,450p,800p,450p_alt,800p_alt,288p,512p,288p_alt,512p_alt"
```

最高1Mbps/1.5Mbps
```
"480p,854p,450p_alt,800p_alt,450p,800p,288p,512p,288p_alt,512p_alt"
```

最高384kbps/450Mbps
```
"288p,512p,288p_alt,512p_alt"
```

最高192kbps/450Mbps
```
"288p_alt,512p_alt,288p,512p"
```
または
```
--default-stream worst
```

### チャンネル、公式のみ録画する  

コピペするように"＊＊＊＊"のように囲ってあります  
＊SlNicoLiveRecの場合は、録画画質→default-streamにコピペした後両端の""を削除してください  
＊**``--default-stream``の引数には``">720p"``のような指定方法はできません**  

最高8Mbps（最高6Mbpsの場合も同じ）  

何も指定しない  
または  
```
--default-stream best
```
または  
```
"1080p,720p,450p,450p_alt,288p,288p_alt"
```

最高3Mbps（最高4Mbpsの場合も同じ）
```
"720p,450p,450p_alt,288p,288p_alt"
```

最高2Mbps
```
"450p,450p_alt,288p,288p_alt"
```

最高1Mbps
```
"450p_alt,450p,288p,288p_alt"
```

最高384kbps
```
"288p,288p_alt"
```

最高192kbps
```
"288p_alt,288p"
```
または  
```
--default-stream worst
```

***
## SlNicoLiveRecで「E-Mail、Password でログインしました」と表示されるが何もしないで終了する  

```
[plugins.nicolive][info] Logging in via provided email and password
E-Mail、Password でログインしました  
---------- Program End Time: 2026/02/10 15:26:18.4817 ----------
```  

### 原因：２段階認証が必要なアカウントでログインしている  
- SlNicoLiveRecは２段階認証オンのアカウントでE-mail/Passwordでログインできません  

### 解決方法  
- ブラウザー(ChromeやFirefoxなど)からCookieのuser_sessionを取得してuser_sessionでログインしてください  
  設定方法は [SlNicoLiveRecで「user_sessionでログイン」に設定する方法](https://nnn-revo2012.github.io/wiki/settings#slnicoliverec%E3%81%A7user_session%E3%81%A7%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AB%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95) を参照  
- ２段階認証をオフにできるアカウントであればオフにしてください（非推奨）  

***
## SlNicoLiveRecで「user_sessionでログイン」に設定する方法  

ニコニコにログインしているブラウザーからuser_sessionというCookieをコピーする必要があります  
他ツールでもuser_sessionを指定できるツールならChromeは6.、NicoGetCookieは7.、直接FirefoxのCookieは8.～9.を他ツールの手順に変換すれば可能です  

**※user_sessionの文字は不用意にインターネット等で公開すると悪意のある第三者が簡単にあなたのアカウントにアクセスできるようになるので公開しないでください**  

### ☆Chromeの場合  

1. Chromeでニコニコにログインする（２段階認証も可能）※既にログインしているなら必要なし  
1. 右上３点マーク→その他のツール→デベロッパーツールを選ぶ  
1. ApplicationメニューのStorage→Cookiesを開き、その中のhttps://www.nicovideo.jp をクリック  
1. するとCookieの一覧表が表示されるので、その中のNameがuser_sessionを探してクリック  
1. 表の下にuser_session_数字_xxxxxxxxxxxx と表示されるのでその行全てをコピー  
1. SlNicoLiveRecの設定→ニコニコアカウント情報で「user_sessionでログイン」を選び、user_sessionの欄に上記でコピーした行全てを貼り付ける 

※Chrome系（Edge、Opera etc）であればメニュー名が違ってても手順はほぼ同じ  

**※user_sessionの文字は不用意にインターネット等で公開すると悪意のある第三者が簡単にあなたのアカウントにアクセスできるようになるので公開しないでください**  

### ☆Firefoxの場合  

### ■NicoGetCookieを使う（おすすめ） 

**Windows専用プログラムですがGUIを使って簡単にuser_sessionを取得できます**  

手順
1. Firefoxでニコニコにログインする（２段階認証も可能）※既にログインしているなら必要なし  
1. NicoGetCookieを [NicoGetCookie/releases](https://github.com/nnn-revo2012/NicoGetCookie/releases) からダウンロードしてください  
1. ダウンロード後zipファイルを解凍し、その中のNicoGetCookie.exeをダブルクリックします  
1. NicoGetCookieが起動します。「ブラウザーから取得」のリストボックスをクリックしてCookieを取得したいブラウザー名を選択してください  
   ブラウザー名の後ろに「（ｘｘｘｘｘ）」と表示されているのが現在ニコニコにログインされているブラウザーです  
   **※Google Chrome、Microsoft Edge、OperaなどのChromium系ブラウザーからのCookie取得はできません**  
1. ブラウザー名の後ろに「（ｘｘｘｘｘ）」と表示されているリストを選んだと同時に「取得結果」の「user_session」の下に「user_session_***************」と表示されればＯＫです  
1. その下の「user_sessionをコピー」ボタンをクリックするとクリップボードにuser_sessionがコピーされます  
1. SlNicoLiveRecの設定→ニコニコアカウント情報で「user_sessionでログイン」を選び、user_sessionの欄に上記でコピーした行全てを貼り付ける  

**※user_sessionの文字は不用意にインターネット等で公開すると悪意のある第三者が簡単にあなたのアカウントにアクセスできるようになるので公開しないでください** 

### ■直接FirefoxのCookieを取得する  

MacやLinuxの場合、NicoGetCookieを使いたくない場合は以下の手順でuser_sessionを取得できます  

1. Firefoxでhttps://www.nicovideo.jp を表示する  
1. Firefoxでニコニコにログインする（２段階認証も可能）※既にログインしているなら必要なし  
1. 右上３点マーク→その他のツール→Web開発ツールを選ぶ  
1. StorageメニューをクリックするとCookieの一覧（ドメイン）が表示される  
1. https://www.nicovideo.jp を探してクリック  
1. 右にCookieの一覧表が表示されるので表の中に名前がuser_sessionとある行をクリック  
1. 更に右にデータと表示され1行目user_sessionの欄の上でコピー  
1. SlNicoLiveRecの設定→ニコニコアカウント情報で「user_sessionでログイン」を選び、user_sessionの欄に上記でコピーした行全てを貼り付ける  
1. コピーした１行の両端に"がついているのでこれを削除（必ずしてください）  

**※user_sessionの文字は不用意にインターネット等で公開すると悪意のある第三者が簡単にあなたのアカウントにアクセスできるようになるので公開しないでください** 

***
## SlNicoLiveRec(Streamlink)で「配信していません」が表示され録画できない  

```
error: No playable streams found on this URL: [ニコ生URL]
配信していません
```  

### 原因１：タイムシフトが見れない状態で接続  
- 以前はタイムシフトが録画できたができなくなった場合  
  - 設定しているuser_sessionが無効になった、アカウントがプレミアから一般になった、ブラウザで"視聴する"ボタンを押してない、一般アカウントで予約していない、タイムシフト期限切れ　など  
- 今回初めてSlNicoLiveRecを設定または再設定の場合  
  - 設定→ニコニコアカウント情報で「ログインしない」になっている、アカウントが一般である、ブラウザで"視聴する"ボタンを押してない、一般アカウントで予約していない、タイムシフト期限切れ　など  

- DEBUGログ：
```
error: No playable streams found on this URL: https://live.nicovideo.jp/watch/lv349598927
配信していません
```  

### 解決方法  
- 以前はタイムシフトが録画できたができなくなった場合  
  - **「設定」→「キャッシュされたログイン資格情報を消去」を有効にしてみてください**  
  - **user_sessionでログインしている場合は、user_sessionを取得しなおしてみてください**  
    設定方法は [SlNicoLiveRecで「user_sessionでログイン」に設定する方法](https://nnn-revo2012.github.io/wiki/settings#slnicoliverec%E3%81%A7user_session%E3%81%A7%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AB%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95) を参照  
  - プレミアム会員か確認してみてください  
  - ブラウザで再生開始してからダウンロードを開始してみてください  
- 今回初めてSlNicoLiveRecを設定または再設定の場合  
  - **設定→ニコニコアカウント情報で「user_sessionでログイン」か「E-Mail、Passwordでログイン」のどちらかに設定してください**  
  - **アカウントが２段階認証オンの場合は必ず「user_sessionでログイン」にしてください**  
  - 「user_sessionでログイン」の設定方法は [SlNicoLiveRecで「user_sessionでログイン」に設定する方法](https://nnn-revo2012.github.io/wiki/settings#slnicoliverec%E3%81%A7user_session%E3%81%A7%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AB%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95) を参照  
  - プレミアム会員か確認してみてください  
  - ブラウザで再生開始してからダウンロードを開始してみてください  

### 原因２：wss_apiに接続して動画のURL(playlist)を取得するまでにタイムアウトした、あるいは拒否された  
- タイムアウト時間はnicolive.py中にSTREAM_READY_TIMEOUT=6(秒)で定義されているが、ニコ生が重くて6秒よりかかることがあるようだ  
  拒否されることもあり得ると思うが不明  
- DEBUGログ：一部抜粋（ログではSTREAM_READY_TIMEOUT=1にして現象を発生させてます）  
```
[plugins.nicolive][debug] Waiting for permit (for at most 1 seconds)...
[plugin.api.websocket][debug] Connected: wss://a.live2.nicovideo.jp/wsapi/v2/watch/lv340299355/timeshift?****
[plugins.nicolive][error] Waiting for permit timed out.
[plugin.api.websocket][debug] Closed: wss://a.live2.nicovideo.jp/wsapi/v2/watch/lv340299355/timeshift?****
error: No playable streams found on this URL: https://live.nicovideo.jp/watch/lv340299355
error: No playable streams found on this URL: https://live.nicovideo.jp/watch/lv340299355
配信していません
```  

### 解決方法  
- しばらく時間を置いてから録画・ダウンロードする  

