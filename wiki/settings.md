# ニコ生向けStreamlink(SlNicoLiveRec)の設定、FAQ  

## 目次  

- ニコニコ生放送で Streamlink --default-stream で指定する画質設定一覧  
- SlNicoLiveRec（Streamlink）で「配信していません」（error: No playable streams found on this URL:）が表示され録画できない  

## ニコニコ生放送で Streamlink --default-stream で指定する画質設定一覧  

コピペするように"＊＊＊＊"のように囲ってあります  
＊SlNicoLiveRecの場合は、録画画質→default-streamにコピペした後両端の""を削除してください  

**ユーザー生のタイムシフトは2026年3月29日まで新旧仕様の画質が混在する**  
**（2026年1月27日までのユーザー生のタイムシフトは旧画質、1月28日以降のタイムシフトは新画質になる）**  

### ユーザー生放送、チャンネル、公式全て録画する人向け  

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

### チャンネル、公式のみ録画する人向け  

コピペするように"＊＊＊＊"のように囲ってあります  
＊SlNicoLiveRecの場合は、録画画質→default-streamにコピペした後両端の""を削除してください  

最高8Mbps（最高6Mbpsの場合も同じ）  

何も指定しない  
または  
```
--default-stream best
```
または  
```
">1080p"
```
または  
```
"1080p,720p,450p,450p_alt,288p,288p_alt"
```

最高3Mbps（最高4Mbpsの場合も同じ）
```
">720p"
```
または  
```
"720p,450p,450p_alt,288p,288p_alt"
```

最高2Mbps
```
">450p"
```
または  
```
"450p,450p_alt,288p,288p_alt"
```

最高1Mbps
```
"450p_alt,450p,288p,288p_alt"
```

最高384kbps
```
">288p"
```
または  
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

## SlNicoLiveRec（Streamlink）で「配信していません」（error: No playable streams found on this URL:）が表示され録画できない

``error: No playable streams found on this URL: [ニコ生URL]``  
``配信していません``  

### 原因１：タイムシフトが見れない状態で接続  
- SlNicoLiveRec（Streamlink）で設定しているuser_sessionが無効になった、タイムシフト期限切れ、一般アカウントでログイン（予約なし）、ブラウザで"視聴する"ボタンを押してないなど  
- DEBUGログ：
```
error: No playable streams found on this URL: https://live.nicovideo.jp/watch/lv349598927
配信していません
```  

### 解決方法  
- プレミアム会員か確認してみてください  
- 「設定」→「キャッシュされたログイン資格情報を消去」を有効にしてみてください  
- user_sessionでログインしている場合は、user_sessionを取得しなおしてみてください  
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

