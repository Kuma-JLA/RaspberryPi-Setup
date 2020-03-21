# RaspberryPi-Setup

```Shell

#仮のユーザ(touryou)を作成する
sudo useradd -M touryou
#touryouをsudoグループに追加
sudo gpasswd -a touryou sudo
#touryouのパスワードを設定
sudo passwd touryou
#ログアウト
exit

sudo apt-get update
sudo apt-get upgrade
sudo passwd root<br>
新しいパスワード:(paassword)<br>
```
