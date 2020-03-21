# RaspberryPi-Setup

デフォルトユーザー"pi"の名前とパスワードを変えるため、GUIを無効化、設定のための仮ユーザーを作成し、piからログアウトする。
```Shell
#GUI無効化
sudo raspi-config
3 Boot Options を選択
B1 Desktop/CLI を選択
B1 Console Text console, requiring user to login  を選択
ここでは再起動せずに設定を続ける。

#仮のユーザー"tmp"を作成する
sudo useradd tmp

#tmpをsudoグループに追加
sudo gpasswd -a tmp sudo

#tmpのパスワードを設定
sudo passwd tmp

#再起動
sudo reboot now
```
<br>
作成したtmpでログインする。<br>
"pi"を"kuma"に変更し、tmpからログアウトする。
```Shell
#"pi"を"kuma"に変更
sudo usermod -l kuma pi

#ホームディレクトリを変更
sudo usermod -d /home/kuma-m kuma

#グループを変更
sudo groupmod -n kuma pi

#再起動
sudo reboot
```
<br>
変更したした"kuma"でログインする。<br>
パスワードは初期設定にて設定した"pi"のパスワード。<br>
仮ユーザーの削除とGUI有効化、sudo使用時のパスワード必須化を行う。
```Shell
#"tmp"を削除
sudo userdel tmp

#GUI有効化
sudo raspi-config
3 Boot Options を選択
B1 Desktop/CLI を選択
B4 Desktop Autologin Desktop GUI, automatically logged in as 'pi' user を選択

#sudo使用時にパスワードが必須になるようにする
sudo rm /etc/sudoers.d/010_pi-nopasswd 
```



```Shell
#
sudo apt-get update
sudo apt-get upgrade
#
sudo apt-get install fonts-note

```
