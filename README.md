# [ja]yt-dlpを使用してBiliBili動画をダウンロードする方法
## ステップ1　必要なツールのダウンロードとか
* [ffmpeg-(version)-full_build.7zまたはffmpeg-(version)-full_build.zip](https://github.com/GyanD/codexffmpeg/releases)をダウンロードし、`%APPDATA%\..\Local`などに解凍する。
* ffmpegの`bin`フォルダを環境変数PATHに登録する。
* [yt-dlp.exe](https://github.com/yt-dlp/yt-dlp-nightly-builds/releases)をダウンロードしてffmpegの`bin`フォルダに移動もしくは`bin`フォルダに直接ダウンロード
* ダウンロード用にフォルダを作っておく(アクセスしやすい場所がおすすめ)
* [Get cookies.txt LOCALLY](https://chromewebstore.google.com/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)をChromeにインストール
* 拡張機能一覧からGet cookies.txt LOCALLYを選択し、Export All Cookiesをクリックして`cookies.txt`をダウンロード用フォルダにダウンロード
## ステップ2　動画をダウンロードするコマンド
* ダウンロード用のフォルダをコマンドプロンプトで開く(Win+R→cmd→`cd ダウンロード用フォルダ`やエクスプローラーでダウンロード用フォルダを開いてF4(アドレスバー)→cmdなど。)
### 単一パートの動画をダウンロード(コマンドプロンプトに記述する形)
```
yt-dlp -f bv+ba --recode-video mp4 --cookies ..\cookies.txt -o OUTPUT.mp4 URL
```
### 複数パートの動画をダウンロード(コマンドプロンプトに記述する形)
```
yt-dlp -f bv+ba --recode-video mp4 --cookies ..\cookies.txt -o "OUTPUT_%(autonumber)03d.mp4" URL

mkdir a

dir /b OUTPUT*>list.txt

for /f "delims=""" %a in (list.txt) do (echo file %a>>list1.txt)

ffmpeg -f concat -i list1.txt -c copy a\OUTPUT.mp4

del OUTPUT*.mp4

del list.txt

del list1.txt

move a\OUTPUT.mp4 .

rmdir /q a\n
```
### 複数パートの動画をダウンロード(バッチファイルに記述する形)
```
yt-dlp -f bv+ba --recode-video mp4 --cookies ..\cookies.txt -o "OUTPUT_%%(autonumber)03d.mp4" URL

mkdir a

dir /b OUTPUT*>list.txt

for /f "delims=""" %%a in (list.txt) do (echo file %%a>>list1.txt)

ffmpeg -f concat -i list1.txt -c copy a\OUTPUT.mp4

del OUTPUT*.mp4

del list.txt

del list1.txt

move a\OUTPUT.mp4 .

rmdir /q a\n
```
必要に応じて`OUTPUT`を変え、`URL`はbilibili動画のURLを使用する。ダウンロードだけなら短縮URLでも可能

# [en]How to download BiliBili videos using yt-dlp
## Step 1. Download tools
