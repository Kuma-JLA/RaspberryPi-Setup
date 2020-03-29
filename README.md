# RaspberryPi-Setup
こちらは余分な説明を抜いたバリカタバージョンです。<br>
Elchikaにはさらにわかりやすく解説したゆるふわバージョンも投稿しましたので是非。<br>
https://elchika.com/article/b0258599-8df9-4017-9490-70ca8c33de5c <br>
<br>
<br>
## "pi"の名前とパスワードを変える
デフォルトユーザー"pi"の名前とパスワードを変えるため、設定のための仮ユーザーを作成し、GUIを無効化してpiからログアウトする。<br>

    #仮のユーザー"tmp"を作成する
    sudo useradd tmp
    
    #tmpをsudoグループに追加
    sudo gpasswd -a tmp sudo
    
    #tmpのパスワードを設定
    sudo passwd tmp

    #GUI無効化
    sudo raspi-config
    3 Boot Options を選択
    B1 Desktop/CLI を選択
    B1 Console Text console, requiring user to login  を選択
    Finish を選択
    再起動する。
    
<br>
作成したtmpでログインする。<br>
"pi"を"kuma"に変更し、tmpからログアウトする。<br>

    #"pi"を"kuma"に変更
    #この際何やら文字化けだらけの何かが表示されるが、Sudo初回実行時に表示されるメッセージである。
    #tmpのパスワードを入力し進める。
    sudo usermod -l kuma pi
    
    #ホームディレクトリを変更
    sudo usermod -d /home/kuma -m kuma
    
    #グループを変更
    sudo groupmod -n kuma pi
    
    #再起動
    sudo reboot

<br>
変更が完了した"kuma"でログインする。<br>
パスワードは初期設定にて設定した"pi"のパスワード。<br>
仮ユーザーを削除しGUIも有効化する。<br>

    #"tmp"を削除
    sudo userdel tmp
    
    #GUI有効化
    sudo raspi-config
    3 Boot Options を選択
    B1 Desktop/CLI を選択
    B4 Desktop Autologin Desktop GUI, automatically logged in as 'pi' user を選択
    7 Advanced Options を選択
    A1 Expand Filesysten を選択
    再起動


## 儀式を執り行う。
少々時間がかかるので注意。<br>

    #パッケージリストをアップデート
    sudo apt-get update
    
    #パッケージをアップデート
    sudo apt-get upgrade
    
    #Google製日本語フォント"Noto"をインストール
    sudo apt-get install fonts-noto
    
    #Google製日本語入力パッケージ"mozc"をインストール
    sudo apt-get install fcitx-mozc


## SSH/VNC/SPI/I2C/Serial を有効化する。

    sudo raspi-config
    5 Interfacing Options を選択
    P2 SSH を選択
    「はい」を選択
    P3,P4,P5,P6も同様に選択
    再起動
    

## SSH/VNCのポート番号変更

### SSH
    sudo nano / etc / ssh / sshd_config

    #Port 22
    ↓
    Port 59090(任意のポート番号に変更してください) 

### VNC
画面右上、RealVNC Serverアイコンをクリックし、表示されたウィンドウの右上の三本線ボタンをクリック、メニューよりOptionsを開く。<br>
表示されたウィンドウ左側の"Conections"を選択すると、右側に"Port:5900"という欄が見つかる。<br>
この"5900"を任意のポート番号に変更する。<br>
<br>

## ファイヤーウォールを設定する。<br>
まずufwをインストール。<br>

    sudo apt-get install ufw
    
ポートを開放するには以下のコマンドを使う。

    sudo ufw allow xxxxx(ポート番号)
    
(例)SSHに指定した"59090"を開放。

    sudo ufw allow 59090
    
ファイヤーウォールを有効化する。

    sudo ufw enable
    
ファイヤーウォールのルールをリロードする。(Piとファイヤーウォールをを起動させたまま開放ポートを追加した後などに使う。)

    sudo ufw reload

解放されているポートを確認する。

    sudo ufw status
