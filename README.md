# RaspberryPi-Setup

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
    sudo usermod -l kuma pi
    #この際何やら文字化けだらけの何かが表示されるが、Sudo初回実行時に表示されるメッセージである。
    #tmpのパスワードを入力し進める。
    
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
    再起動

<br>
儀式を執り行う。<br>
少々時間がかかるので注意。<br>

    #パッケージリストをアップデート
    sudo apt-get update
    
    #パッケージをアップデート
    sudo apt-get upgrade
    
    #Google製日本語フォント"Noto"をインストール
    sudo apt-get install fonts-noto
    
    #Google製日本語入力パッケージ"mozc"をインストール
    sudo apt-get install fcitx-mozc
